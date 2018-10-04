# Cloud Firestore Transactions

A transaction is a set of read and write operations on one or more Cloud Firestore documents that execute in a single atomic operation - either all of the operations succeed, or none of them are applied.

Transactions are useful when you want to update a field's value based on it's current value or the value of some other field. For example you could increment a counter by creating a transaction that reads the current value of the counter, increments it, and writes the new value to Cloud Firestore.

A transaction can consist of any number of `get()` operations followed by any number of write operations using methods such as `set()`, `update()` and `delete()`.

## Caveats

When using transactions the following points should be kept in mind:

- **Transactions** will **fail** when the client is **offline**.
- **Read** operations are **asynchronous** (Promises).
- Your **updateFunction** **can return** a **Promise**.
- **Write** operations are **synchronous** but don't apply until after your `updateFunction` has finished executing.
- Your transaction `updateFunction` might run more than once if a concurrent edit affects a document that the transaction reads.
- Transaction `updateFunction` should not directly modify react state, you'd do this in the result of the transaction.

## Examples

### Increment a value

This example demonstrates incrementing a number transactionally even if a doc does not already exist and then returning the new value as the transaction result.

```javascript
import firebase from 'react-native-firebase';

const ref = firebase.firestore().collection('cities').doc('London');

firebase
  .firestore()
  .runTransaction(async transaction => {
    const doc = await transaction.get(ref);

    // if it does not exist set the population to one
    if (!doc.exists) {
      transaction.set(ref, { population: 1 });
      // return the new value so we know what the new population is
      return 1;
    }

    // exists already so lets increment it + 1
    const newPopulation = doc.data().population + 1;

    transaction.update(ref, {
      population: newPopulation,
    });

    // return the new value so we know what the new population is
    return newPopulation;
  })
  .then(newPopulation => {
    console.log(
      `Transaction successfully committed and new population is '${newPopulation}'.`
    );
  })
  .catch(error => {
    console.log('Transaction failed: ', error);
  });
```


### Abort a transaction

This example extends on the previous example and aborts the transaction if the population is greater than 5.

```javascript
import firebase from 'react-native-firebase';

const ref = firebase.firestore().collection('cities').doc('London');

firebase
  .firestore()
  .runTransaction(async transaction => {
    const doc = await transaction.get(ref);

    // if it does not exist set the population to one
    if (!doc.exists) {
      transaction.set(ref, { population: 1 });
      // return the new value so we know what the new population is
      return 1;
    }

    // exists already so lets increment it + 1
    const newPopulation = doc.data().population + 1;

    if (newPopulation <= 5) {
      transaction.update(ref, {
        population: newPopulation,
      });
    } else {
      // returning a promise reject will abort the transaction
      return Promise.reject(new Error('Population too big!'));
    }

    // return the new value so we know what the new population is
    return newPopulation;
  })
  .then(newPopulation => {
    console.log(
      `Transaction successfully committed and new population is '${newPopulation}'.`
    );
  })
  .catch(error => {
    if (error.message.includes('too big')) {
      // Population too big - handle this specific error
    } else {
      console.log('Transaction failed: ', error);
    }
  });
```

### Multiple reads and writes

This is an advanced example that demonstrates multiple reads and writes on multiple document references.

In this example we will increment the population of `London` and increment the population of the `United Kingdom` based on the totals of the cities.

```javascript
import firebase from 'react-native-firebase';

const refA = firebase.firestore().collection('cities').doc('London');
const refB = firebase.firestore().collection('cities').doc('Manchester');
const refC = firebase.firestore().collection('cities').doc('Nottingham');
const refD = firebase.firestore().collection('countries').doc('United Kingdom');

const updateFunction = async transaction => {
  const [londDoc, mancDoc, nottDoc, ukDoc] = await Promise.all([
    transaction.get(refA),
    transaction.get(refB),
    transaction.get(refC),
    transaction.get(refD),
  ]);

  // + 1 on London population as we're also incrementing it
  const londPop = londDoc.exists ? londDoc.data().population + 1 : 1;

  // only using these for UK total
  const mancPop = mancDoc.exists ? mancDoc.data().population : 0;
  const nottPop = nottDoc.exists ? nottDoc.data().population : 0;

  // set or update London population
  if (!londDoc.exists) {
    transaction.set(refA, { population: londPop });
  } else {
    transaction.update(refA, {
      population: londPop,
    });
  }

  // set or update UK population
  const totalPop = londPop + mancPop + nottPop;
  if (!ukDoc.exists) {
    transaction.set(refD, { population: totalPop });
  } else {
    transaction.update(refD, {
      population: totalPop,
    });
  }

  // return the values so we can log them in the transaction result promise
  return {
    london: londPop,
    manchester: mancPop,
    nottingham: nottPop,
    uk: totalPop,
  };
};

// run the transaction
firebase
  .firestore()
  .runTransaction(updateFunction)
  .then(result => {
    console.log(result);
    // OUTPUTS:
    //  { london: 1, manchester: 0, nottingham: 0, uk: 1 }
  })
  .catch(error => {
    console.log('Transaction failed: ', error);
  });
```
