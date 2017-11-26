# hatch-template-project - Farmchain

This template project should be forked by hatch teams.

This project was developed during [hatchlondon 2017](http://hatchlondon.io).

## Todo

Tick items off as you go along.

- [x] 1. [Sign up](https://help.github.com/articles/signing-up-for-a-new-github-account/) for a free GitHub account
- [x] 2. [Fork](https://help.github.com/articles/fork-a-repo/) this project
- [x] 3. Add your forked repo from `step 2` to this [project](https://github.com/SheCanCodeHQ/hatchlondon-2017-projects) as a [Pull Request](https://help.github.com/articles/about-pull-requests/)

### Project setup

From now on it is in your **Forked** repo

- [x] 4. At the top of your **repo** add a brief project description & link to where it is hosted.

![Repo description and link](https://user-images.githubusercontent.com/624760/33160443-57e86a96-d014-11e7-8488-52592fc69a81.png)

*TIP: [GitHub Pages](https://pages.github.com) gives free static website hosting*

### README changes (this file)

- [x] 5. Change the name at the top of this file on `line 1`
- [x] 6. Under the name of this project put a brief description of the project `line 3` (this can be more detailed than `step 4`)
- [x] 7. Fill in your team members in the **TEAM** section below
- [x] 8. Fill in the **PROBLEM AND SOLUTION** section below
- [x] 9. Fill in the **INSTALL AND RUN THIS PROJECT** section below
- [x] 10. Any *digital / paper* notes you make during the hackathon you MUST add to the **Issue** section in your repo

*TIP: drag and drop [images / photos](https://help.github.com/articles/file-attachments-on-issues-and-pull-requests/)*

## Team

Include all members of your team for the hack here:

* Michelle Lam [github](link to github profile)
* Polina Olemskaia [github](link to github profile)
* Ilya Kleyner [github](link to github profile)
* Wing Vasiksiri [github](link to github profile)

## Problem and Solution

Describe here which problem you are working on during the event, and what your solution is, succinctly.

## Install and run this project

import java.util.ArrayList;
import java.util.Scanner;

public class FarmChain {

	public static void main(String[] args) {
		Scanner stdIn = new Scanner(System.in);
		ArrayList<Block> blockchain = new ArrayList<>();
		int currentBlockchainIndex = 0;
		String legibleLedger = ""; //This would, of course, be written to a file in a full implementation
		
		Transaction genesisTransaction1 = new Transaction("Ilya", "Wing", 50, new Animal[] {new Animal("cow", 10, 725.0, "Smith's Farm, Texas", "0000"), new Animal("chicken", 3, 4.5, "Farm A", "0001")});
		String genesisTransaction1String = genesisTransaction1.toString();
		legibleLedger += genesisTransaction1.addToLedger();
		Transaction genesisTransaction2 = new Transaction("Polina", "Michelle", 2, new Animal[]{new Animal("unicorn", 2, 99, "Iowa Dairy Farm", "0002")});
		String genesisTransaction2String = genesisTransaction2.toString();
		legibleLedger += genesisTransaction2.addToLedger();
		Transaction genesisTransaction3 = new Transaction("Wing", "Ilya", 100, new Animal[] {new Animal("cow", 10, 725, "Missouri Dairy Farm", "0003"), new Animal("goat", 3, 10,"Missouri Dairy Farm", "0004"), new Animal("turkey", 2, 2.5, "Missouri Dairy Farm", "0005")});
		String genesisTransaction3String = (genesisTransaction3).toString();
		legibleLedger += genesisTransaction3.addToLedger();
		String[] genesisTransactions = {genesisTransaction1String, genesisTransaction2String, genesisTransaction3String};
		
		Block genesisBlock = new Block(0, genesisTransactions);
		blockchain.add(genesisBlock);
		currentBlockchainIndex++;
		
		boolean anotherTransaction = false;
		System.out.print("Would you like to enter a transaction (y/n)? ");
		if (stdIn.nextLine().charAt(0) == 'y') {
			anotherTransaction = true;
		}
		
		String[] blockNTransactionStrings = new String[3];
		int transactionNumber = 1;
		
		String sellerName, buyerName;
		double price;
		Animal[] animals;
		int numberOfAnimals;
		
		while (anotherTransaction == true) {
			System.out.print("Enter the seller's username: ");
			sellerName = stdIn.nextLine();
			System.out.print("Enter the buyer's username: ");
			buyerName = stdIn.nextLine();
			System.out.print("How many animals were sold? ");
			numberOfAnimals = stdIn.nextInt();
			stdIn.nextLine();
			animals = new Animal[numberOfAnimals];
			
			String type;
			String AnimalId;
			double age;
			double weight;
			String location;
			for (int i=0; i<animals.length; i++) {
				System.out.print("Enter Animal #" + (i + 1) + "'s type: ");
				type = stdIn.nextLine();
				System.out.print("Enter Animal #" + (i + 1) + "'s  ID: ");
				AnimalId = stdIn.nextLine();
				System.out.print("Enter Animal #" + (i + 1) + "'s age (years): ");
				age = stdIn.nextDouble();
				System.out.print("Enter Animal #" + (i + 1) + "'s weight (kg): ");
				weight = stdIn.nextDouble();
				stdIn.nextLine();
				System.out.print("Enter Animal #" + (i + 1) + "'s location: ");
				location = stdIn.nextLine();
				
				animals[i] = new Animal(type, age, weight, location, AnimalId);
			}
			System.out.print("Enter the price for those animals ($): ");
			price = stdIn.nextDouble();
			stdIn.nextLine();
			
			Transaction blockNTransactionM = new Transaction(sellerName, buyerName, price, animals);
			legibleLedger += blockNTransactionM.addToLedger();
			blockNTransactionStrings[transactionNumber] = blockNTransactionM.toString();
			transactionNumber++;
			if (transactionNumber == 3) {
				blockchain.add(new Block(blockchain.get(currentBlockchainIndex-1).getBlockHash(), blockNTransactionStrings));
				currentBlockchainIndex++;
				transactionNumber = 0;
			}
			
			System.out.print("Would you like to enter another Transaction (y/n)? ");
			if (stdIn.nextLine().charAt(0) == 'n') {
				anotherTransaction = false;
			}
			
			if (anotherTransaction == false && transactionNumber != 0) {
				switch (transactionNumber) {
				case 1:
					String[] oneTransactionString = new String[1];
					oneTransactionString[0] = blockNTransactionStrings[0];
					blockchain.add(new Block(blockchain.get(currentBlockchainIndex-1).getBlockHash(), oneTransactionString));
					currentBlockchainIndex++;
					break;
				case 2:
					String[] twoTransactionStrings = new String[2];
					twoTransactionStrings[0] = blockNTransactionStrings[0];
					twoTransactionStrings[1] = blockNTransactionStrings[1];
					blockchain.add(new Block(blockchain.get(currentBlockchainIndex-1).getBlockHash(), twoTransactionStrings));
					currentBlockchainIndex++;
					break;
				}
			}
		}
		
		System.out.println();
		for (int i=0; i<currentBlockchainIndex; i++) {
			System.out.println(blockchain.get(i).getBlockHash());
		}
		
		System.out.println();
		System.out.println(legibleLedger);
		
	}

}
