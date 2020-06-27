#pragma once
#include <iostream>
using namespace std;
class kyhieu
{
protected:
	float truongdo;
public:
	virtual void nhap();
	virtual bool ladaulangden();
	virtual int laycaodo() = 0;
};
void kyhieu::nhap()
{
	int t; 
	cout << "nhap gia tri truong do:";
	cout << "1.tron 2.trang 3.den 4.moc don";
	cout << "5.moc kep 6.moc tam 7.moc tu";
	cin >> t;
	switch (t)
	{
	case 1: truongdo = 4;
		break;
	case 2: truongdo = 2;
		break;
	case 3: truongdo = 1;
		break;
	case 4: truongdo = 0.5;
		break;
	case 5: truongdo = 0.25;
		break;
	case 6: truongdo = 0.125;
		break;
	case 7: truongdo = 0.0625;
		break;
	}
}
bool kyhieu::ladaulangden()
{
	return false;
}
class notnhac :public kyhieu
{
private:
	int caodo;
public:
	void nhap();
	int laycaodo();
};
void notnhac::nhap()
{
	int t;
	cout << "nhap gia tri cao do:";
	cout << "1.do(C) 2.re(D) 3.mi(E) 4.fa(F)";
	cout << "5.sol(G) 6.la(A) 7.si(B)";
	cin >> t;
	caodo = t;
	kyhieu::nhap();
}
int notnhac::laycaodo()
{
	return caodo;
}
class daulang :public kyhieu
{
public:
	bool ladaulangden();
	int laycaodo();
};
bool daulang::ladaulangden()
{
	if (truongdo == 1)
		return true;
	return false;
}
int daulang::laycaodo()
{
	return 0;
}
void main()
{
	kyhieu* bannhac[50];
	int n;
	cout << "nhap vao so luong cac ky hieu am nhac";
	cin >> n;
	for (int i = 0; i<n; i++)
	{
		int t;
		cout << "chon1 de soan not nhac";
		cout << "va 2 de soan dau lang";
		cin >> t;
		switch (t)
		{
		case 1: bannhac[i] = new notnhac();
			break;
		case 2: bannhac[i] = new daulang();
			break;
		}
		bannhac[i]->nhap();
	}
	int count = 0;
	for (int i = 0; i < n; i++)
		if (bannhac[i]->ladaulangden() == true)
			count++;
	cout << "so dau lang den la" << count;
	int max = bannhac[0]->laycaodo();
	int vt = 0;
	for (int i = 0; i<n; i++)
		if (bannhac[i]->laycaodo() > max)
		{
			max = bannhac[i]->laycaodo();
			vt = i;
		}
	cout << "vi tri not nhac co cao do nhat:" << vt;
}
