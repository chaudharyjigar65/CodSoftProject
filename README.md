# CodSoftProject
//Number Guessing Game
import java.util.Scanner;
import java.util.Random;
 class NumberGuessingGame {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);
        Random random = new Random();

        int secretNumber = random.nextInt(100) + 1;
        int attempts = 0;
        int guess;

        System.out.println("Welcome to the Number Guessing Game!");
        System.out.println("Thinking of a number between 1 and 100.");

        do {
            System.out.print("Take a guess: ");
            guess = input.nextInt();
            attempts++;

            if (guess < secretNumber) {
                System.out.println("Too low! Try again.");
            } else if (guess > secretNumber) {
                System.out.println("Too high! Try again.");
            } else {
                System.out.println("Congratulations! You guessed the number in " + attempts + " attempts.");
            }
        } while (guess != secretNumber);
       
    }
}

//Currency Converter
import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.text.DecimalFormat;

 class Currency_Converter extends JFrame {
    final JLabel amountLabel, fromLabel, toLabel, resultLabel;
    final JTextField amountField;
    final JComboBox<String> fromComboBox, toComboBox;
    final JButton convertButton;
    final DecimalFormat decimalFormat = new DecimalFormat("#,##0.00");

    private final String[] currencies = {"USD", "EUR", "JPY", "GBP", "CAD", "AUD", "CHF", "CNY","INR"};
    final double[] exchangeRates = {1.00, 0.84, 109.65, 0.72, 1.27, 1.30, 0.92, 6.47,87.14};

    public Currency_Converter() {
        setTitle("Currency Converter");
        setLayout(new GridLayout(4, 2));

        amountLabel = new JLabel("Amount:");
        add(amountLabel);

        amountField = new JTextField();
        add(amountField);

        fromLabel = new JLabel("From:");
        add(fromLabel);

        fromComboBox = new JComboBox<>(currencies);
        add(fromComboBox);

        toLabel = new JLabel("To:");
        add(toLabel);

        toComboBox = new JComboBox<>(currencies);
        add(toComboBox);

        convertButton = new JButton("Convert");
        add(convertButton);

        resultLabel = new JLabel();
        add(resultLabel);

        convertButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                try {
                    double amount = Double.parseDouble(amountField.getText());
                    String fromCurrency = (String) fromComboBox.getSelectedItem();
                    String toCurrency = (String) toComboBox.getSelectedItem();
                    double exchangeRate = exchangeRates[getIndex(toCurrency)] / exchangeRates[getIndex(fromCurrency)];
                    double result = amount * exchangeRate;
                    resultLabel.setText(decimalFormat.format(result) + " " + toCurrency);
                } catch (Exception ex) {
                    resultLabel.setText("Invalid input");
                }
            }
        });

        setSize(300, 200);
        setVisible(true);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
    }

    private int getIndex(String currency) {
        for (int i = 0; i < currencies.length; i++) {
            if (currency.equals(currencies[i])) {
                return i;
            }
        }
        return -1;
    }

    public static void main(String[] args) {
        new Currency_Converter();
    }
}

//ATM Machine
package com.ATMMachine;

import java.util.Scanner;

public class ATM {
    float balance;
    int PIN = 3449;

    public void checkPin() {
        System.out.print("Enter your Pin : ");
        Scanner in = new Scanner(System.in);
        int enteredPin = in.nextInt();
        if (enteredPin == PIN) {
            menu();
        } else {
            System.out.println("Enter a Valid Pin.. ");
        }
    }

    public void menu() {
        System.out.println(" Enter Your Choice ");
        System.out.println("1. Check A/C Balance ");
        System.out.println("2. Withdraw Money ");
        System.out.println("3. Deposit Money ");
        System.out.println("4. EXIT ");

        Scanner in = new Scanner(System.in);
        int opt = in.nextInt();

        if (opt == 1) {
            checkBalance();
        } else if (opt == 2) {
            withdrawMoney();
        } else if (opt == 3) {
            depositMoney();
        } else if (opt == 4) {
            return;
        } else {
            System.out.println("Enter a Valid Choice ");
            menu();
        }
    }

    public void checkBalance(){
        System.out.println("Balance : "+balance);
        menu();
    }
    public void withdrawMoney(){
        System.out.println("Enter Amount To Withdraw : ");
        Scanner in = new Scanner(System.in);
        float amount=in.nextFloat();
        if(amount>balance){
            System.out.println("Insufficient Balance ");
        }else {
            balance=balance-amount;
            System.out.println("Money Withdraw Successfully ");
        }
        menu();
    }

    public void depositMoney(){
        System.out.println("Enter The Amount : ");
        Scanner in =new Scanner(System.in);
        float amount=in.nextFloat();
        balance=balance+amount;
        System.out.println("Money Deposited Successfully ");
        menu();
    }

    public void checkpin(){
      menu();
    }
}
