# Beginner-BlackJack
This was a blcak jack game I created for my final assigment my python class
# Name: Mitchell Barnett
# Purpose: Simulates games of blackjack
# Date: Nov 27, 2020

from datetime import *
import random

#randomly picks a number betwen 1-10
#retuns the random number
def pick_a_card():
    card_values = [
        1,2,3,
        4,5,6,
        7,8,9,
        10,]
    card = random.choice(card_values)
    return card

def main():
    dash="-"
    #asks if you would like to start a game
    while True:
        start_game = input("Would you like to play a game of BlackJack? (y/n):  ")
        valid_start = str.isalpha(start_game)
        if valid_start == True:
            if start_game in ("Y","y"):
                print("\nLets begin")
                break
            elif start_game in ("N","n"):
                sys.exit(0)
            else:
                print("\nError: Please enter y or n")
        if valid_start == False:
            print("\nError: Please enter only letters")

    #start core game loop
    while True:
        #picks 2 random card for the dealer and player
        #adds up player and dealer stater score
        player_card_1 = pick_a_card()
        player_card_2 = pick_a_card()
        dealer_card_1 = pick_a_card()
        dealer_card_2 = pick_a_card()
        player_blackjack = player_card_1 + player_card_2
        dealer_blackjack = dealer_card_1 + dealer_card_2

        print("\nPlayer")
        print("\nYou got a", player_card_1, "and an", player_card_2)
        print("\nYour sum is", player_blackjack)
        print("\nDealer has an", dealer_card_1, "and a Hidden Card")

        #adds the card score up and asks for hit or stay for the player
        while True:
            hit_card = pick_a_card()
            if player_blackjack == 21:
                print("\nCONGRATULATIONS!")
                print("\nYOU GOT BLACKJACK!")
                break
            if player_blackjack > 21:
                print("\nPlayer Busts")
                break
            possible_hit = input("\nPlayer! hit or stay (h/s):    ")
            valid_hit = str.isalpha(possible_hit)
            if valid_start == True:
                if possible_hit in ("H","h"):
                    print("\nYou got an", hit_card)
                    player_blackjack += hit_card
                    print("\nYour new Total is ", player_blackjack)
                elif possible_hit in ("S","s"):
                    print("\nYour total is", player_blackjack)
                    break
                else:
                    print("\nError: Please enter h or s")
            if possible_hit == False:
                print("\nError: Please enter only letters")

        print("\nThe dealer revals the hidden card")
        print("\nDealer has an", dealer_card_1, "and an", dealer_card_2)
        print("\nDealer sum is ", dealer_blackjack)

        #adds the card score up and chooses hit or stay for the dealer
        while True:
            hit_card = pick_a_card()
            if player_blackjack > 21:
                break
            if dealer_blackjack > 21:
                print("\nDealer Busts")
                break
            if (dealer_blackjack >= 17 and
                dealer_blackjack <=21):
                print("\nDealer stays")
                break
            if dealer_blackjack <= 16:
                print("\nDealer hit")
                print("\nDealer got an", hit_card)
                dealer_blackjack += hit_card
                print("\nDealer's total is ", dealer_blackjack)

        #determines if the player or the dealer wins
        if (dealer_blackjack > 21 and
            player_blackjack <= 21):
            print("\nPlayer WINS")
        elif (player_blackjack > dealer_blackjack and
            player_blackjack <= 21):
            print("\nPlayer WINS")
        else:
            print("\nThe Dealer WINS")
        print(f"\n{dash:-^49}")

        #asks to play again
        while True:
            end_game = input("\nWould you like to play again (y/n):  ")
            valid_end = str.isalpha(end_game)
            if valid_end == True:
                if end_game in ("Y","y"):
                    print("\nLets begin")
                    break
                elif end_game in ("N","n"):
                    print("\nThanks for playing")
                    sys.exit(0)
                else:
                    print("\nError: Please enter y or n")
            if valid_end == False:
                print("\nError: Please enter only letters")
main()

