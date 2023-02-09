#include <iostream>
#include <fstream>
#include <string>
#include <vector>
#include <random>
#include <chrono>
#include <thread>
#include <iomanip>
#include <cstdlib>

int main() {

std::cout << "autor programu: Grzegorz Dziuba, Nr indeksu : 22430" << std::endl;//

    start:// etykieta start, możemy do niej wrócić za pomocą goto
        int counter = 0;  // zmienna licznikowa, ustawiana na 0
    std::string fileName = ("C:\\Users\\g.dziuba\\Pictures\\WSB\\projekt\\projekt\\slowa.txt");//deklaracja zmiennej filename dla pliku  tekstowego ze slowami
    std::ifstream file(fileName);//otwarcie pliku o podanej nazwie
    std::vector<std::string> words;// wektor, w którym będą przechowywane słowa z pliku
    std::string word;//deklaracja zmiennej word

    int choice;

std::cout << "Witaj w grze polegajacej na odgadnieciu slowa!" << std::endl;// wyświetlamy tekst menu z opcjami do wyboru
std::cout << "Wybierz jedna z opcji:" << std::endl;
std::cout << "1. Graj samodzielnie" << std::endl;
std::cout << "2. Graj z przyjacielem" << std::endl;//wyswietlamy tekst //menu
std::cout << "3. Wyswietl liste slow mozliwych do odgadniecia" << std::endl;
std::cin >> choice; //// użytkownik wprowadza swój wybór za pomocą zmiennej choice, która jest potem używana w instrukcji switch


    if (!file) {// Sprawdzanie, czy plik zostal poprawnie otwarty, w przypadku bledu wyswietlenie komunikatu "szubienica" i zakonczenie programu
        std::cerr << "szubienica" << std::endl;
        return 1;
    }
    // Wczytanie slow z pliku do wektora

    while (std::getline(file, word)) {// Petla wczytujaca slowa z pliku do wektora words
        words.push_back(word);
    }

    file.close();// Zamykanie pliku po wczytaniu slow
    std::random_device rd;// Inicjalizacja generatora liczb losowych
    std::mt19937 generator(rd());
    std::uniform_int_distribution<int> distribution(0, words.size()-1);// Inicjalizacja rozkladu jednostajnego dla generatora liczb losowych z zakresu od 0 do rozmiaru wektora words-1 (poniewaz indeksy sa liczone od 0)

    std::string wordToGuess; //zmienne
    std::string userGuess; //zmienne


        switch(choice){//tutaj jest switch do naszego menu
        case 1://opcja do gry samemu, ponizej kod ktory odpala gre
        system("cls");
        while (true) {// Pętla główna gry, w której użytkownik będzie podawał swoje odgadywania
            std::cout << "Wybrales opcje gry samemu, sprobuj odgadnac haslo z losowych liter" << std::endl;
            std::cout << "Aby wrocic do wyboru trybu gry wpisz menu" << std::endl;
            for (int i = 0; i < 3; i++) {
                std::cout << ".";
                std::this_thread::sleep_for(std::chrono::milliseconds(500));
            }
            std::cout << std::endl;
            std::cout << std::endl;
std::string wordToGuess = words[distribution(generator)]; // losujemy słowo z naszej listy
std::string hiddenWord(wordToGuess.size(), '_'); // tworzymy łańcuch z "_" o długości słowa do odgadnięcia


while (hiddenWord != wordToGuess && userGuess != "menu") {
    std::cout << "Slowo do odgadniecia: " << hiddenWord << std::endl;
    std::cout << "Podaj litere: " <<std::endl;

    std::cin >> userGuess;

    if (userGuess == "menu") {// Sprawdzamy czy użytkownik chce powrócić do menu

        goto start;// przeskakujemy do etykiety "start"
    }
// Sprawdzamy czy odgadywanie jest poprawne
    bool correctGuess = false; // deklaracja zmiennej bool correctGuess, która będzie mówić czy odgadnięto poprawnie literę czy nie
    for (int i = 0; i < wordToGuess.size(); i++) {//rozpoczęcie pętli for, która przebiega tyle razy ile jest liter w słowie do odgadnięcia
        if (wordToGuess[i] == userGuess[0]) { //sprawdzenie czy litera z userGuess jest taka sama jak litera w wordToGuess na pozycji i
            hiddenWord[i] = userGuess[0];//jeśli tak, to zamiana podkreślnika na odgadniętą literę w hiddenWord oraz ustawienie correctGuess na true (oznacza to, że odgadnięto literę)
            correctGuess = true;
        }
    }



    if (!correctGuess) {
        counter++;
        std::cout << "Podana litera nie wystepuje w slowie, sprobuj ponownie." << std::endl;

    if (counter == 1) {
        std::cout << "    _________" << std::endl;
        std::cout << "   |         |" << std::endl;
        std::cout << "   |         O" << std::endl;
    } else if (counter == 2) {
        std::cout << "    _________" << std::endl;
        std::cout << "   |         |" << std::endl;
        std::cout << "   |         O" << std::endl;
        std::cout << "   |        /|\\" << std::endl;
    } else if (counter == 3) {
        std::cout << "    _________" << std::endl;
        std::cout << "   |         |" << std::endl;
        std::cout << "   |         O" << std::endl;
        std::cout << "   |        /|\\" << std::endl;
        std::cout << "   |         |" << std::endl;
    } else if (counter == 4) {
        std::cout << "    _________" << std::endl;
        std::cout << "   |         |" << std::endl;
        std::cout << "   |         O" << std::endl;
        std::cout << "   |        /|\\" << std::endl;
        std::cout << "   |         |" << std::endl;
        std::cout << "   |        / " << std::endl;
    } else if (counter == 5) {
        std::cout << "    _________" << std::endl;
        std::cout << "   |         |" << std::endl;
        std::cout << "   |         O" << std::endl;
        std::cout << "   |        /|\\" << std::endl;
        std::cout << "   |         |" << std::endl;
        std::cout << "   |        / \\" << std::endl;
        std::cout << "   |" << std::endl;
        std::cout << "   |" << std::endl;
        std::cout << "___|___" << std::endl;
    } else if (counter == 6){//Jeśli licznik odpowiedzi błędnych użytkownika osiągnie 6, wyświetla się komunikat o przegranej oraz prawidłowe hasło. Następnie program czeka przez 5 sekund i czyści ekran przed powrotem do menu głównego.
        std::cout << "przegrales! slowo do odgadniecia bylo....: " << wordToGuess << std::endl;
        std::this_thread::sleep_for(std::chrono::seconds(5));
        system("cls");
        goto start;
        }


    } else if (userGuess == wordToGuess) {
        std::cout << "Gratulacje! Odgadles slowo: " << wordToGuess << std::endl;
            std::this_thread::sleep_for(std::chrono::seconds(2));
            system("cls");
    break;

    } else if (hiddenWord == wordToGuess) {
    std::cout << "Gratulacje! Odgadles slowo: " << wordToGuess << std::endl;
    std::this_thread::sleep_for(std::chrono::seconds(2));
    system("cls");
    break;
    }
    }
    }
//Kod powyżej sprawdza, czy podane przez użytkownika słowo jest takie same jak słowo do odgadnięcia. Jeśli tak, wyświetla się komunikat "Gratulacje! Odgadłeś słowo: [słowo do odgadnięcia]" i gra kończy się. Jeśli użytkownik odgadł słowo poprzez uzupełnienie wszystkich liter w ciągu z "_" na odpowiednie litery, to również wyświetlany jest komunikat o zwycięstwie i gra kończy się.
    case 2://gra z przyjacielem
{
    std::cout << "Wybrales opcje gry z przyjacielem, gracz nr 1 wybiera slowo, gracz 2 probuje je odgadnac" << std::endl;
    std::cout << "Gracz 1, wybierz slowo do odgadniecia:" ;
    std::cin >> wordToGuess;
    std::string hiddenWord(wordToGuess.size(), '_');
//Gracz nr 1 wybiera słowo do odgadnięcia, a gracz nr 2 próbuje je odgadnąć. Komunikat "Wybrales opcje gry z przyjacielem, gracz nr 1 wybiera slowo, gracz 2 probuje je odgadnac" pojawia się na początku, a następnie gracz 1 jest proszony o wybranie słowa do odgadnięcia. Następnie, w pętli while, jest wyświetlane słowo do odgadnięcia z ukrytymi literami, a gracz nr 2 jest proszony o podanie litery. Jeśli użytkownik wpisze "menu" gracz wróci do początku programu.
    while (hiddenWord != wordToGuess && userGuess != "menu") {
        std::cout << "Slowo do odgadniecia: " << hiddenWord << std::endl;
        std::cout << "Graczu nr 2, podaj litere: " <<std::endl;
        std::cin >> userGuess;

        if (userGuess == "menu") {
            goto start;
        }

        bool correctGuess = false; // zmienna do sprawdzania czy odgadnięta litera jest w słowie
        for (int i = 0; i < wordToGuess.size(); i++) {
            if (wordToGuess[i] == userGuess[0]) { // porównujemy tylko pierwszą literę
                hiddenWord[i] = userGuess[0];
                correctGuess = true;
            }
        }


    if (!correctGuess) {
        counter++;
        std::cout << "Podana litera nie wystepuje w slowie, sprobuj ponownie." << std::endl;

    if (counter == 1) {
        std::cout << "    _________" << std::endl;
        std::cout << "   |         |" << std::endl;
        std::cout << "   |         O" << std::endl;
    } else if (counter == 2) {
        std::cout << "    _________" << std::endl;
        std::cout << "   |         |" << std::endl;
        std::cout << "   |         O" << std::endl;
        std::cout << "   |        /|\\" << std::endl;
    } else if (counter == 3) {
        std::cout << "    _________" << std::endl;
        std::cout << "   |         |" << std::endl;
        std::cout << "   |         O" << std::endl;
        std::cout << "   |        /|\\" << std::endl;
        std::cout << "   |         |" << std::endl;
    } else if (counter == 4) {
        std::cout << "    _________" << std::endl;
        std::cout << "   |         |" << std::endl;
        std::cout << "   |         O" << std::endl;
        std::cout << "   |        /|\\" << std::endl;
        std::cout << "   |         |" << std::endl;
        std::cout << "   |        / " << std::endl;
    } else if (counter == 5) {
        std::cout << "    _________" << std::endl;
        std::cout << "   |         |" << std::endl;
        std::cout << "   |         O" << std::endl;
        std::cout << "   |        /|\\" << std::endl;
        std::cout << "   |         |" << std::endl;
        std::cout << "   |        / \\" << std::endl;
        std::cout << "   |" << std::endl;
        std::cout << "   |" << std::endl;
        std::cout << "___|___" << std::endl;

    } else if (counter == 6){
        std::cout << "przegrales! slowo do odgadniecia bylo....: " << wordToGuess << std::endl;
            std::this_thread::sleep_for(std::chrono::seconds(5));
            system("cls");
            goto start;

            }

}}}
   case 3: {
        std::cout << "Lista dostepnych slow:" << std::endl;
        std::cout << std::left << std::setw(10) << "Nr" << std::setw(20) << "Słowo" << std::endl;
        for (int i = 0; i < words.size(); i++) {
            std::cout << std::left << std::setw(10) << i+1 << std::setw(20) << words[i] << std::endl;
        }
        goto start;
    }
    default:
        std::cout << "Wybrano niepoprawna opcje" << std::endl;
        break;
}

return 0;
}


