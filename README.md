# Jeu-de-l-oie
package fr.gouv.finances.exo;

import java.util.Random;
import java.util.Scanner;

public class jeuDeLoie {

    public static void main(String[] args) {
	// crée deux variables pour les 2 dés (des1, des2)
	// crée deux variables pour les 2 utilisateurs(uti1, uti 2)
	// cree une variable avec le jet double (doubleJet)
	// Interdit de s'arreter sur les cases multiples de 9 et si on tombe
	// Jeu qui tourne autour des conditions
	// crée des variables pour chaque cases/obstacles indiqués dans le jeu

	int des1 = d6();
	int des2 = d6();
	int emplct1 = 1;
	int emplct2 = 1;
	int joueurUn = 1;
	int joueurDeux = 1;
	int caseFin = 63;
	String nomJoueur1, nomJoueur2;
	int TourDeJeu = 1;
	int premierJet1;
	int premierJet2;
	boolean bloque1 = true;
	boolean bloque2 = true;
	boolean caseNormale = false;

	Scanner saisie = new Scanner(System.in);
	System.out.println("Premier joueur, quel est votre nom ?");
	nomJoueur1 = saisie.nextLine();
	System.out.println("Deuxième joueur, quel est votre nom ?");
	nomJoueur2 = saisie.nextLine();
	premierJet1 = d6() + d6();
	System.out.println("Jet du joueur 1 : " + premierJet1);
	premierJet2 = d6() + d6();
	System.out.println("Jet du joueur 2 : " + premierJet2);

	if (premierJet1 < premierJet2) {
	    String nomJoueur3 = nomJoueur1;
	    nomJoueur1 = nomJoueur2;
	    nomJoueur2 = nomJoueur3;
	}

	System.out.println(nomJoueur1 + " commence !");

	while (emplct1 != caseFin && emplct2 != caseFin) {

	    System.out.println("Tour " + TourDeJeu);
	    System.out.println(nomJoueur1 + " en case  " + emplct1);
	    System.out.println(nomJoueur2 + " en case  " + emplct2);

	    if (bloque1 != true) {
		emplct1 = jet(emplct1, TourDeJeu);
		if (emplct1 == 19) {
		    bloque1 = true;
		    System.out.println("Le joueur est bloqué");
		} else {
		    bloque1 = false;
		}
		if (bloque2 != true) {
		    emplct2 = jet(emplct2, TourDeJeu);
		    if (emplct2 == 19) {
			bloque2 = true;
			System.out.println("Le joueur est bloqué");
		    }

		} else {
		    bloque2 = false;
		}

	    }

	    if (emplct1 > caseFin) {
		emplct1 = caseFin - (emplct1 - caseFin);
	    }

	    if (emplct2 > caseFin) {
		emplct2 = caseFin - (emplct2 - caseFin);

	    }
	    System.out.println(nomJoueur1 + " arrive en " + emplct1);
	    System.out.println(nomJoueur2 + " arrive en " + emplct2);
	    TourDeJeu++;

	}
	saisie.close();
    }

    static int d6() {
	Random rand = new Random();
	int resDé = rand.nextInt(6) + 1;
	return resDé;
    }

    static int jet(int emplct, int tourDeJeu) {
	int resDé1 = d6();
	int resDé2 = d6();
	emplct = emplct + resDé1 + resDé2;

	if (tourDeJeu == 1) {

	    if ((resDé1 == 6 && resDé2 == 3) || (resDé1 == 3 && resDé2 == 6)) {
		emplct = 26;
		System.out.println("Vous avez fait 6 et 3, vous allez à la case " + emplct);
	    }
	    if ((resDé1 == 4 && resDé2 == 5) || (resDé1 == 5 && resDé2 == 4)) {
		emplct = 53;
		System.out.println("Vous avez fait 4 et 5, vous allez à la case " + emplct);
//	    } else {
//		System.out.println("Vous commencez à une case normale ou vous êtes bloquez");
//	    }

	    }
	    if (emplct == 6) {
		System.out.println("Il y a un pont, allez à la case " + emplct);
		emplct = 12;
	    }
	    if (0 == emplct % 9) {
		emplct = emplct + resDé1 + resDé2;
		System.out.println("Vous êtes sur une case bénéfique " + emplct);

	    }
	    if (emplct == 19) {
		emplct = resDé1 + resDé2 + resDé1 + resDé2;
		System.out.println("Il y l'hôtel, vous vous reposez et autre joueur joue 2 fois");

	    }
	    if (emplct == 31) {
		System.out.println("Il y a un puits, il faut attendre de le relever");
		emplct = 31;

	    }
	    if (emplct == 42) {
		System.out.println("Il y a un labyrinthe, retournez à la case " + emplct);
		emplct = 34;
	    }

	    if (emplct == 58) {
		emplct = 1;
		System.out.println("C'est la mort vous recommencez à la case " + emplct);
	    }

	}
	return emplct;
    }

}
