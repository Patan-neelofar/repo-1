import java.util.ArrayList;
import java.util.Scanner;

// Base class: Account
class Account {
    private String accountNumber;
    private String name;
    private double balance;

    public Account(String accountNumber, String name, double initialDeposit) {
        this.accountNumber = accountNumber;
        this.name = name;
        this.balance = initialDeposit;
    }

    public String getAccountNumber() {
        return accountNumber;
    }

    public String getName() {
        return name;
    }

    public double getBalance() {
        return balance;
    }

    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            System.out.println("✅ Deposited: ₹" + amount);
        } else {
            System.out.println("❌ Invalid deposit amount!");
        }
    }

    public void withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
            System.out.println("✅ Withdrawn: ₹" + amount);
        } else {
            System.out.println("❌ Insufficient balance or invalid amount!");
        }
    }

    public void displayInfo() {
        System.out.println("\nAccount Number: " + accountNumber);
        System.out.println("Name: " + name);
        System.out.println("Balance: ₹" + balance);
    }
}

// Bank class manages multiple accounts
class Bank {
    private ArrayList<Account> accounts = new ArrayList<>();

    public void createAccount(String accountNumber, String name, double initialDeposit) {
        Account acc = new Account(accountNumber, name, initialDeposit);
        accounts.add(acc);
        System.out.println("✅ Account created successfully!");
    }

    public Account findAccount(String accountNumber) {
        for (Account acc : accounts) {
            if (acc.getAccountNumber().equals(accountNumber)) {
                return acc;
            }
        }
        return null;
    }

    public void displayAllAccounts() {
        if (accounts.isEmpty()) {
            System.out.println("No accounts found!");
            return;
        }
        for (Account acc : accounts) {
            acc.displayInfo();
            System.out.println("--------------------");
        }
    }
}

// Main class
public class BankManagementSystem {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        Bank bank = new Bank();
        int choice;

        do {
            System.out.println("\n====== BANK MANAGEMENT SYSTEM ======");
            System.out.println("1. Create Account");
            System.out.println("2. Deposit Money");
            System.out.println("3. Withdraw Money");
            System.out.println("4. Check Balance");
            System.out.println("5. Display All Accounts");
            System.out.println("0. Exit");
            System.out.print("Enter your choice: ");
            choice = sc.nextInt();

            switch (choice) {
                case 1:
                    System.out.print("Enter Account Number: ");
                    String accNo = sc.next();
                    System.out.print("Enter Name: ");
                    String name = sc.next();
                    System.out.print("Enter Initial Deposit: ");
                    double deposit = sc.nextDouble();
                    bank.createAccount(accNo, name, deposit);
                    break;

                case 2:
                    System.out.print("Enter Account Number: ");
                    accNo = sc.next();
                    Account acc = bank.findAccount(accNo);
                    if (acc != null) {
                        System.out.print("Enter Amount to Deposit: ");
                        double amt = sc.nextDouble();
                        acc.deposit(amt);
                    } else {
                        System.out.println("❌ Account not found!");
                    }
                    break;

                case 3:
                    System.out.print("Enter Account Number: ");
                    accNo = sc.next();
                    acc = bank.findAccount(accNo);
                    if (acc != null) {
                        System.out.print("Enter Amount to Withdraw: ");
                        double amt = sc.nextDouble();
                        acc.withdraw(amt);
                    } else {
                        System.out.println("❌ Account not found!");
                    }
                    break;

                case 4:
                    System.out.print("Enter Account Number: ");
                    accNo = sc.next();
                    acc = bank.findAccount(accNo);
                    if (acc != null) {
                        acc.displayInfo();
                    } else {
                        System.out.println("❌ Account not found!");
                    }
                    break;

                case 5:
                    bank.displayAllAccounts();
                    break;

                case 0:
                    System.out.println("👋 Thank you for using Bank Management System!");
                    break;

                default:
                    System.out.println("❌ Invalid choice!");
            }
        } while (choice != 0);

        sc.close();
    }
}
