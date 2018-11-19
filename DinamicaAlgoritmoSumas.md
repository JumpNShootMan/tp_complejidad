```c++
#pragma once
#include <iostream>
#include <fstream>
#include <string>
#include <vector>
using namespace std;
class Centros {
private:
	int cod;
	bool sale;
	bool entra;
	float x, y;
public:
	Centros() {
		cod = NULL;
		x = y = NULL;
		entra = sale = false;
	}
	Centros(int cod, float x, float y) {
		this->cod = cod;
		this->x = x;
		this->y = y;
	 }
	float getx() {
		return x;
	}
	float gety() {
		return y;
	}
	int getcod() {
		return cod;
	}
	bool getsale() {
		return sale;
	}
	bool getentra() {
		return entra;
	}
	void setentra() {
		entra = true;
	}
	void setsale() {
		sale = true;
	}
	
};

 
void copiarvalores(vector<Centros> &arreglo) {

	ifstream ip("CentrosPoblados.txt");
	if (!ip.is_open()) cout << "El archivo ya esta abierto" << endl;
	for (int i = 0; i < arreglo.size(); i++)
	{
		arreglo.push_back(Centros(ip.getline(ip, arreglo[i].getcod(), ';'),
			ip.getline(ip, arreglo[i].getx(), ';'),
			ip.getline(ip, arreglo[i].gety(), ';')));
	}
}
float difx(Centros x, Centros y) {
	float diff;
	if (x.getx()>y.getx()) {
		diff = (x .getx()- y.getx());
	}	
	else if (y.getx()>x.getx()) {
		diff = (y.getx() - x.getx());
	}
	else if (x.getx() == y.getx()) {
		diff = 0;
	}
	return diff;
}

float dify(Centros x, Centros y) {
	float diff;
	if (x.gety()>y.gety()) {
		diff = (x.gety() - y.gety());
	}
	else if (y.gety()>x.gety()) {
		diff = (y.gety() - x.gety());
	}
	else if (x.gety() == y.gety()) {
		diff = 0;
	}
	return diff;
}

vector<Centros> arreglo(145225);

int rec() {

}

void recorrer(vector<Centros> &arreglo, int i) {
	float menorx, menory, menorz;
	int coordenadamenor;
	float sumamenor;
	Centros auxx, auxy, auxz;
	int posicion1, posicion2, posicion3;
	menorz = menory = menorx = 100000000000;
	for (int i; i < i + 1; i++) {
		for (int j = i + 1; j < 145225; j++) {
			if (arreglo[j].getentra() == false) {
				if (difx(arreglo[i], arreglo[j]) < menorx) {
					menorx = arreglo[j].getx();
					auxx = arreglo[j];
					posicion1 = j;
				}
			}
		}

		float suma1 = difx(arreglo[i], arreglo[posicion1]) + dify(arreglo[i], arreglo[posicion1]);


		for (int k = i + 1; k < 145225; k++) {
			if (dify(arreglo[i], arreglo[k]) < menory) {
				menory = arreglo[k].gety();
				auxy = arreglo[k];
				posicion2 = k;
			}
		}

		float suma2 = dify(arreglo[i], arreglo[posicion2]) + dify(arreglo[i], arreglo[posicion2]);

		if (suma2 < suma1) {
			coordenadamenor = posicion2;
			sumamenor = suma2;
		}
		else{

			coordenadamenor = posicion1;
			sumamenor = suma1;
		}
		
		arreglo[coordenadamenor].setentra();
	}
	
	cout << "El arreglo con codigo: " << arreglo[i].getcod() << " se junta con el arreglo con codigo: " 
		<< arreglo[coordenadamenor].getcod() << " con una diferencia en distancia de: " << sumamenor << endl;

	
	i += 1;
	if (i == arreglo.size()-1) { return; }
	else {
		recorrer(arreglo, i);
	}
}
```
