# Tutorial 1

## Summary

In our first tutorial, we're going to build a functioning ATM application. And yes, this will be a graphical application. No, you're not done with Swing just yet.

Users will be allowed to login to their accounts, view their balance, as well as deposit, withdraw, or transfer funds. Don't worry, we're going to walkthrough it together before I turn you loose on your own.

## Model

Let's start with the model. Remember, applications are all about data. What entities will we need to model for an ATM application? If we zoom all the way out, there's really only two.

* Users
* Bank accounts

As we start to design our application, these entities will become the primary classes of our program. In the real world, we'd likely track much more than we're going to in this tutorial. This is more to get the feel of how to build an application from scratch.

Let's start with the `User` class.

* First name
* Last name
* Email address
* Phone number
* Bank account

That's good for now. To keep things simple, we'll pretend that users only have one bank account.

{% code title="User.java" %}
```java
package org.ucvts.model;

public class User {

    private String firstName;
    private String lastName;
    private String emailAddress;
    private long phoneNumber;
    private BankAccount account;
    
    /**
     * Create a new User with a default BankAccount.
     * 
     * @param firstName
     * @param lastName
     * @param emailAddress
     * @param phoneNumber
     */
    
    public User(String firstName, String lastName, String emailAddress, long phoneNumber) {
        this.firstName = firstName;
        this.lastName = lastName;
        this.emailAddress = emailAddress;
        this.phoneNumber = phoneNumber;
        
        this.account = new BankAccount();
    }
    
    public String getFirstName() {
        return firstName;
    }
    
    public String getLastName() {
        return lastName;
    }
    
    public String getEmailAddress() {
        return emailAddress;
    }
    
    public long getPhoneNumber() {
        return phoneNumber;
    }
    
    public BankAccount getAccount() {
        return account;
    }
}

```
{% endcode %}

Pretty straightforward, right? The `User` class doesn't do a whole lot. We'll call upon it to provide us with data, but the business logic is going to live in the `BankAccount` class.

* Account number
* Balance

Sure, there are almost certainly more things that a real bank account would track, but this is good for the purposes of this tutorial.

{% code title="BankAccount.java" %}
```java
package org.ucvts.model;

public class BankAccount {

    private static long nextAccountNumber = 10000001L;
    
    private long accountNumber;
    private BigDecimal balance;
    
    /**
     * Creates a BankAccount with the next available account number, and
     * a starting balance of 0.00.
     */
    
    public BankAccount() {
        this.accountNumber = BankAccount.nextAccountNumber++;
        this.balance = new BigDecimal(0);
    }
    
    public long getAccountNumber() {
        return accountNumber;
    }
    
    public BigDecimal getBalance() {
        return balance;
    }
}

```
{% endcode %}

We're doing some different things here that you may not have seen before, so let's take the time to slow down and wrap our heads around it. First, the `accountNumber` and `nextAccountNumber`. What are these and why do we need both?

`accountNumber` is going to represent the account number of each user's account. It will be unique. `nextAccountNumber` is static, and therefore all instances of the `BankAccount` class share its value. Changing it from one class changes it for all classes. This allows us to use it to keep the next available account number queued up. Whenever we create a new account, we assign it this `nextAccountNumber` value before incrementing it by one.

And what about `BigDecimal`? Well, that's a built-in class designed for currencies \(or really whenever exact precision is needed\). As I'm sure you've seen in some of the Java problem sets, sometimes a `double` has weird rounding errors. This isn't acceptable in financial applications, so we use something that isn't plagued with those problems.

I said the business logic would be handled by the BankAccount class, so let's add that in now. We need to be able to deposit, withdraw, and transfer funds. Deposits and withdrawals are easy, since we just need to update the balance. Transfers will require another bank account. We'll layout the broad strokes, but we'll need to come back later to finish the job.

{% code title="BankAccount.java" %}
```java
package org.ucvts.model;

import java.math.BigDecimal;

import org.ucvts.ATM;

public class BankAccount {

    private static long nextAccountNumber = 10000001L;
    
    private long accountNumber;
    private BigDecimal balance;
    
    /**
     * Creates a BankAccount with the next available account number, and
     * a starting balance of 0.00.
     */
    
    public BankAccount() {
        this.accountNumber = BankAccount.nextAccountNumber++;
        this.balance = new BigDecimal(0);
    }
    
    public long getAccountNumber() {
        return accountNumber;
    }
    
    public BigDecimal getBalance() {
        return balance;
    }
    
    /**
     * Deposits funds into this account.
     * 
     * @param amount - the amount to deposit
     * @return a status code indicating the result of the deposit
     */
    
    public int deposit(BigDecimal amount) {
        if (amount.compareTo(BigDecimal.ZERO) <= 0) {
            return ATM.INVALID;
        } else {
            balance = balance.add(amount);
        }
        
        return ATM.SUCCESS;
    }
    
    /**
     * Withdraws funds from this account.
     * 
     * @param amount - the amount to withdraw
     * @return a status code indicating the result of the withdrawal
     */
    
    public int withdraw(BigDecimal amount) {
        if (amount.compareTo(BigDecimal.ZERO) <= 0) {
            return ATM.INVALID;
        } else {
            BigDecimal temp = balance;
            
            if (temp.subtract(amount).compareTo(BigDecimal.ZERO) < 0) {
                return ATM.INSUFFICIENT;
            } else {
                balance = balance.subtract(amount);
            }
        }
        
        return ATM.SUCCESS;
    }
    
    /**
     * Transfers funds from this account to another account.
     * 
     * @param destination - the destination account
     * @param amount - the amount to transfer
     * @return a status code indicating the result of the transfer
     */
    
    public int transfer(BankAccount destination, BigDecimal amount) {        
        int status = this.withdraw(amount);
        
        if (status == ATM.SUCCESS) {
            return destination.deposit(amount);
        } else {
            return status;
        }
    }
}

```
{% endcode %}

If you're following along, which you should be, your code won't compile just yet. Don't worry, we'll get to that. First, let's make sure we understand the three methods we just added to the `BankAccount` class.

* **`deposit`**

The `deposit` method performs an obvious job. It puts money into the account.

```java
/**
  * Deposits funds into this account.
  * 
  * @param amount - the amount to deposit
  * @return a status code indicating the result of the deposit
  */

public int deposit(BigDecimal amount) {
    if (amount.compareTo(BigDecimal.ZERO) <= 0) {
        return ATM.INVALID;
    } else {
        balance = balance.add(amount);
    }
    
    return ATM.SUCCESS;
}
```

First, we need to check that the `amount` we're trying to deposit is valid. We don't want to accept negative numbers or zero, which is what the `if` statement verifies. If the `amount` is less than or equal to zero, we return a status code indicating that the amount wasn't valid. You'll see where those are defined next.

If the `amount` is valid, then we update the `balance` using the `add` method from the `BigDecimal` class. Afterwards, we return a success status code.

* **`withdraw`**

Like the `deposit` method, the `withdraw` method is equally intuitive. It takes money out of the account.

```java
/**
  * Withdraws funds from this account.
  * 
  * @param amount - the amount to withdraw
  * @return a status code indicating the result of the withdrawal
  */

public int withdraw(BigDecimal amount) {
    if (amount.compareTo(BigDecimal.ZERO) <= 0) {
        return ATM.INVALID;
    } else {
        if (balance.subtract(amount).compareTo(BigDecimal.ZERO) < 0) {
            return ATM.INSUFFICIENT;
        } else {
            balance = balance.subtract(amount);
        }
    }
        
    return ATM.SUCCESS;
}
```

We need to do the same check as the `deposit` method. The `amount` has to be a positive, non-zero value, otherwise we return an invalid status code.

Unique to the withdraw method, we also need to verify that we have enough money in the account to perform the transaction. Here's how we're doing that.

The `BigDecimal` methods \(e.g., `add` or `subtract`\) don't actually modify the calling object unless we explicitly set the return value to the caller. To clarify, the following line will tell us what the result of the transaction will be without actually modifying `balance`.

```java
if (balance.subtract(amount).compareTo(BigDecimal.ZERO) < 0) {
    return ATM.INSUFFICIENT;
}
```

So, if the `if` statement is `true` and the result of the transaction would be a negative `balance`, then we know we don't have enough money and should return an insufficient funds status code. Otherwise, we're free to actually modify the `balance`. We use the same call to the `subtract` method in the `BigDecimal` class, except we set `balance` equal to the return value to capture the change.

* **`transfer`**

While we'll need to come back to this method a bit later to verify the existence of the `destination` account, the functionality of transferring boils down to simply withdrawing from one account and depositing into another. We can reuse the methods we already have in place.

```java
/**
  * Transfers funds from this account to another account.
  * 
  * @param destination - the destination account
  * @param amount - the amount to transfer
  * @return a status code indicating the result of the transfer
  */

public int transfer(BankAccount destination, BigDecimal amount) {        
    int status = this.withdraw(amount);
    
    if (status == ATM.SUCCESS) {
        return destination.deposit(amount);
    } else {
        return status;
    }
}
```

First, we want to withdraw from the original account, which is `this` account. We capture the status code from the return value of the `withdraw` method. If we were able to successfully perform the withdrawal, we proceed with depositing the funds into the `destination` account.

If you're paying attention, you'll see that I used `this.withdraw` and `destination.deposit`. Using `this` wasn't necessary, but it clarifies that I am withdrawing money from the current account. Using `destination` when calling deposit is required, otherwise the money wouldn't go to the right place.

All of the verifications against amount are handled by the `deposit` and `withdraw` methods. Later, we'll come back and add a check that the `destination` account actually exists.

## View

TODO

## Controller

TODO

