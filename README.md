#include <iostream>

#include <cstdlib>

#include <ctime>

int getRandomNumber(int min, int max)

{

	static const double fraction = 1.0 / (static_cast<double>(RAND_MAX) + 1.0);

	return static_cast<int>(rand() * fraction * (max - min + 1) + min);

}

bool playGame(int guesses, int number, int min, int max)

{

	for (int count = 1; count <= guesses; ++count)

	{

		std::cout << " Попытка #" << count << ": ";

		int guess;

		std::cin >> guess;

		while (guess > max || guess < min)

		{

			std::cout << " Ты совсем ебанутый, введи нормальное число: ";

			std::cin >> guess;

		}

		if (guess > number)

		{

			std::cout << " Твое число больше загаданного.\n";

		}

		else if (guess < number)

		{

			std::cout << " Твое число меньше загаданного числа.\n";

		}

		else

		{

			return true;

		}

	}

	return false;

}

bool playAgain()

{

	char ch;

	do

	{

		std::cout << " Сыграем еще раз: (y/n)? ";

		std::cin >> ch;

	} while (ch != 'y' && ch != 'n');

	return (ch == 'y');

}

int main()

{

	srand(static_cast<unsigned int>(time(0)));

	const int guesses = 7;

	int min, max;

	do

	{

		std::cout << " Введи диапазон генерации чисел\n";

		std::cout << " Минимальное число: ";

		std::cin >> min;

		std::cout << " Максимальное число: ";

		std::cin >> max;

		while (max <= min)

		{

			std::cout << " Че, самый умный? \n";

			std::cout << " Максимальное число: ";

			std::cin >> max;

		}

		int number = getRandomNumber(min, max);

		std::cout << " У тебя есть " << guesses << " попыток, чтобы отгадать число.\n";

		bool won = playGame(guesses, number, min, max);

		if (won)

		{

			std::cout << " Верно, поздравляю.\n";

		}

		else

		{

			std::cout << " Не угадал, правильное число - " << number << "\n";

		}

	} while (playAgain());

	std::cout << " Спасибо за игру.\n";

	return 0;

}
