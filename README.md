# testt


#include <iostream>
#include <fstream>
#include<string>
#include <Windows.h>
using namespace std;

struct human
{
	string  FIO;
	string num;
	int summ = 0;
};

struct operation
{
	string data;
	string num_P;
	string oper;
	string summ_of_remainder;

	void del()
	{
		oper = " ";
		summ_of_remainder = " ";

	}
};
int main()
{
	setlocale(LC_ALL, "rus");
	SetConsoleCP(1251);
	SetConsoleOutputCP(1251);

	const int m = 3;
	string procedure = "withdrawal";
	fstream client;
	string path ;
	cout << "введите файл с клиентами:" << endl;
	cin >> path;
	client.open(path, fstream::in | fstream::out | fstream :: app);
	if (!client.is_open())
	{
		cout << "ошибка открытия 1 файла  " << endl;
		return 0;
	}

	else
	{
		cout << "файл с данными клиента открыт" << endl;


		//заполняем 
		human people[m];
		for (int i = 0; client; i++)
		{
			client >> people[i].FIO;
			client >> people[i].num;
			client >> people[i].summ;
		}

		client.close();

		fstream fin_op;
		string n_file ;
		cout << "введите файл с операциями клиентов: " << endl;
		cin >> n_file;
		fin_op.open(n_file, fstream::in | fstream::out | fstream::app);
		if (!fin_op.is_open())
		{
			cout << "ошибка открытия 2 файла  " << endl;
			return 0;

		}
		else
		{
			cout << "файл с операциями открыт  " << endl;

			const int x = 3;
			operation action[x];
			// заполняем 
			for (int o = 0; fin_op; o++)
			{
				fin_op >> action[o].oper;
				fin_op >> action[o].data;
				fin_op >> action[o].num_P;
				fin_op >> action[o].summ_of_remainder;
			}

			fin_op.close();

			///                                                <начинается менюшка>
			int f;
			cout << "введите значение меню:" << "  " << endl;
			cin >> f;

			switch (f)
			{
			case 1:
			{
				cout << " выберите нужного клиента банка по номеру счета: " << endl;
				cout << " в нашем банке пока только 3 клиента, по этому впишите номер от ( 01 до 03 )" << endl;

				string compare;
				cin >> compare;

				for (int v = 0; v < x; v++)
				{
					if (compare == people[v].num)
					{
						cout << people[v].FIO << endl;
						cout << people[v].summ << endl;;
					}
				}

				for (int p = 0; p < x; p++)
				{

					if (compare == action[p].num_P)
					{
						cout << action[p].data << endl;
						cout << action[p].oper << endl;
						cout << action[p].summ_of_remainder << endl;
					}
				}
				break;
			}

			case 2:
			{
				// выввод всех операций по выбранному номеру.
				cout << " выберите того, чию операцию хотите увидеть: " << endl;
				string compare2;
				cin >> compare2;
				for (int v = 0; v < x; v++)
				{
					if (compare2 == people[v].num)
					{
						cout << people[v].FIO << endl;
					}
				}
				for (int p = 0; p < x; p++)
				{

					if (compare2 == action[p].num_P)
					{
						cout << action[p].oper << endl;
					}
				}
				break;
			}
			case 3:
			{
				int l;
				cout << "что делаем ? " << endl;
				cout << "1- меняем операцию" << endl;
				cout << "2 - добавляем " << endl;
				cin >> l;
				switch (l)
				{

				case 1:
				{
					cout << " ИЗМЕНЕНИЯ ДАННЫХ ПОЛЬЗОВАТЕЛЯ: " << endl;
					cout << " кого хотите изменить введите банковский счет" << endl;
					string counter3;
					cout << "введите counter3 " << endl;
					cin >> counter3;
					for (int a = 0; a < x; a++)
					{
						if (counter3 == action[a].num_P)
						{
							action[a].del();
							cout << "измените вид операции" << endl;
							cin >> action[a].oper;
							cout << "смениет сумму" << endl;
							cin >> action[a].summ_of_remainder;
							cout << "выводим всю информацию по даному клиенту: " << endl;
							cout << people[a].FIO << endl;
							cout << action[a].num_P << endl;
							cout << action[a].data << endl;
							cout << action[a].oper << endl;
							cout << action[a].summ_of_remainder << endl;

							// загоняем данные в файл 

							fin_op.open(n_file, fstream::in | fstream::out | fstream::trunc | fstream :: app);
							for (int q = 0; q < m; q++)
							{
								fin_op << action[q].oper << endl;
								fin_op << action[q].data << endl;
								fin_op << action[q].num_P << endl;
								fin_op << action[q].summ_of_remainder << endl;

							}
							fin_op.close();
						}

					}
					break;
				}
				case 2:
				{
					cout << "добавляем данные пользователю: " << endl;

					string counter4;
					cout << "введите counter4 " << endl;
					cin >> counter4;

					for (int a = 0; a < x; a++)
					{
						if (counter4 == people[a].num)
						{
							if (counter4 == action[a].num_P)
							{
								cout << "вводим дополнительную операцию: " << endl;
								string dop_op;
								string dop_sum;
								cout << " введите операции " << endl;
								cin >> dop_op;
								cout << " сумму " << endl;
								cin >> dop_sum;
								action[a].summ_of_remainder = action[a].summ_of_remainder + ", " + dop_sum;
								action[a].oper = action[a].oper + ", " + dop_op;
								// вывод соединенных операций 

								cout << people[a].FIO << endl;
								cout << action[a].oper << endl;
								cout << action[a].summ_of_remainder << endl;

								/*
								// вывели данные по нужному клиенту с добавленой операцией.
								cout << people[a].FIO << endl;//
								cout << action[a].data << endl;
								cout << action[a].oper << ", " + dop_op << endl;
								cout << action[a].summ_of_remainder << ", " + dop_sum << endl;*/

								// перевести данные по новой сумме операции в инт и вывести новое( финальное значение суммы на счету)


								cout << "конечная сумма на счету  " << endl;
								int SUM = stoi(dop_sum); //перевели в инт 
								if (dop_op == procedure)
								{
									people[a].summ = people[a].summ - SUM;
									cout << " остаток с выводом средств  " << endl;
									cout << people[a].summ << endl;
								}
								else
								{
									people[a].summ = people[a].summ + SUM;
									cout << " остаток с пополнением счета  " << endl;
									cout << people[a].summ << endl;
								}


								client.open(path, fstream::in | fstream::out | fstream::trunc | fstream::app);
								for (int w = 0; w < m; w++)
								{
									client << people[w].FIO << endl;
									client << people[w].num << endl;
									client << people[w].summ << endl;
								}
								client.close();

								fin_op.open(n_file, fstream::in | fstream::out | fstream::trunc | fstream::app);
								for (int q = 0; q < m; q++)
								{
									fin_op << action[q].oper << endl;
									fin_op << action[q].data << endl;
									fin_op << action[q].num_P << endl;
									fin_op << action[q].summ_of_remainder << endl;

								}
								fin_op.close();
							}

						}

					}
					break;
				}
				default:
					cout << " ошибка введения  " << endl;
					break;
				}
			}
			default:
				break;
			}


		}


	}

}

