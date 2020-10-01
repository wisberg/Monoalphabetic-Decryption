# Monoalphabetic-Decryption
Monoalphabetic Decryption Helper
//
//  main.cpp
//  Monoalphabetic Decryption Helper
//
//  Created by Duff Isberg on 2020.
//  Copyright (c) 2020 Duff Isberg. All rights reserved.
//

#include <iostream>
#include <string>
using namespace std;

class letters{
public:
    int letter;
    double frequency = 0;
    double percentage;
};

void letterSearch(char findLetter, letters Alphabet[])
{
    int findLetterNum = static_cast<int>(findLetter);
    
    for(int i = 0; i<26; i++)
    {
        if(Alphabet[i].letter == findLetterNum)
        {
            Alphabet[i].frequency++;
        }
    }
}



int main()
{
    letters englishPercent[26];
    //Set an array with the frequencies in alphabetical order, then set this englishPercent array to each percent with a for loop. Then sort them in ascending like you did below then youl be able to output the letter with its frequency for comparison
    double ePercents[26] =
    {8.167,
    1.492,
    2.782,
    4.253,
    12.702,
    2.228,
    2.015,
    6.094,
    6.966,
    0.153,
    0.772,
    4.025,
    2.406,
    6.749,
    7.507,
    1.929,
    0.095,
    5.987,
    6.327,
    9.056,
    2.758,
    0.978,
    2.361,
    0.150,
    1.974,
    0.074};
    
    
    cout<<"Welcome to the Frequency Analysis Calculator for Monoalphebetic Substitution Cyphers!"<<endl;
    cout<<"*******************************************************"<<endl;
    letters cypherAlphabet[26];
    for(int i = 0; i <26; i++)
    {
        cypherAlphabet[i].letter = i+65;
    }
    
    for(int i = 0; i <26; i++)
    {
        englishPercent[i].letter = i+65;
    }
    
    for (int i = 0; i<26; i++)
    {
        englishPercent[i].frequency = ePercents[i];
    }
    
    string cypherMessage = "";
    char repeat = 'y';
    while(repeat == 'y')
    {
    
    unsigned long length(0);
    cout<<"Enter the cypher message in capitals here: "<<endl;
    getline(cin,cypherMessage);
    length = cypherMessage.length();
    int emptySpaces = 0;
    
    for (int i=0;i<length;i++)
    {
        if(cypherMessage[i] == ' ')
        {
            emptySpaces++;
        }
    }
    
        
    double letterLength = length - emptySpaces;
    
    
    for(int j = 0; j<length;j++)
    {
        letterSearch(cypherMessage[j], cypherAlphabet);
    }
        
        //Setting Percentage Values//
        for(int i = 0; i<26;i++)
        {
            cypherAlphabet[i].percentage = (cypherAlphabet[i].frequency/letterLength)*100;
        }
        
        //Sorting//
        letters temp;
        for(int i = 0; i<26;i++)
        {
            for (int j = 0; j<26; j++)
            {
                if (cypherAlphabet[j].percentage < cypherAlphabet[i].percentage)
                {
                    temp = cypherAlphabet[i];
                    cypherAlphabet[i] = cypherAlphabet[j];
                    cypherAlphabet[j] = temp;
                }
            }
        }
        
        letters temp2;
        for(int i = 0; i<26;i++)
        {
            for (int j = 0; j<26; j++)
            {
                if (englishPercent[j].frequency < englishPercent[i].frequency)
                {
                    temp2 = englishPercent[i];
                    englishPercent[i] = englishPercent[j];
                    englishPercent[j] = temp2;
                }
            }
        }

        
        
    //Outputting in Order//
        cout<<"-------------------------------------------------------"<<endl;
        cout<<"Cypher Letter Percents   |   English Language Percents"<<endl;
        
    for(int i = 0; i<26;i++)
    {
        char letterName = static_cast<char>(cypherAlphabet[i].letter);
        char englishLetter = static_cast<char>(englishPercent[i].letter);
        cout<<letterName<<": "<<cypherAlphabet[i].percentage<<"%"<<"                    "<<englishLetter<<": "<<englishPercent[i].frequency<<"%"<<endl;
    }
        
        
        
        cout<<"Repeat? (y/n)"<<endl;
        cin>>repeat;
        repeat = tolower(repeat);
        
    }
    
}
