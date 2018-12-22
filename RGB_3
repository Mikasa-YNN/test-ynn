//ヘッダーファイルにstdafx.hを追加、windwsデスクトップウィザードで空のプロジェクトを作成する
#include "stdafx.h"
#include <atlimage.h>
#include <iostream>
#include <stdio.h>
#include <windows.h>
using namespace std;

int xw = -1920;

BOOL  CALLBACK  EnumWndProc(HWND hWnd, LPARAM lParam)
{
	char buff[256] = "";
	GetWindowText(hWnd, buff, sizeof(buff));
	if (strcmp(buff, (char*)lParam) == 0) {//名前が一致したら、
		SetWindowPos(hWnd, HWND_TOP, -8 + xw, -31, 600, 300, SWP_SHOWWINDOW);//ウインドウの位置とサイズを変更
	}
	return true;
}


int main(int argc, char* argv[])
{

	int exit;
	int R, G, B;
	int Rave, Gave, Bave;
	COLORREF color;
	HWND hWnd;
	HDC hWndDC;

	LPARAM lParam = (LPARAM)"Minecraft 1.12.2";//検索するウィンドウの名前
	EnumWindows(EnumWndProc, (LPARAM)lParam);

	// キャプチャしたいデスクトップの矩形
	CRect targetRect(xw, 0, 600, 300);

	hWnd = GetDesktopWindow();

	for (int i = 0; i < 100000; i++) {
		hWndDC = GetDC(hWnd);

		// DIBSECTIONの作成
		CImage img;
		img.Create(targetRect.Width(), targetRect.Height(), 24);
		CImageDC imgDC(img);

		// デスクトップ画像をDIBSECTIONへ転送
		BitBlt(imgDC, 0, 0, targetRect.Width(), targetRect.Height(), hWndDC, targetRect.left, targetRect.top, SRCCOPY);

		// 各種開放
		ReleaseDC(hWnd, hWndDC);

		// ここからのアクセスは、もう少し高速化できないこともない
		for (int pixy = 0; pixy < 16; pixy++) {
			for (int pixx = 0; pixx < 32; pixx++) {
				color = img.GetPixel(pixx * 18 + 17, pixy * 18 + 5);
				Rave = GetRValue(color);
				Gave = GetGValue(color);
				Bave = GetBValue(color);
				color = img.GetPixel(pixx * 18 + 17, pixy * 18 + 11);
				Rave = GetRValue(color);
				Gave = GetGValue(color);
				Bave = GetBValue(color);
				color = img.GetPixel(pixx * 18 + 23, pixy * 18 + 5);
				Rave = GetRValue(color);
				Gave = GetGValue(color);
				Bave = GetBValue(color);
				color = img.GetPixel(pixx * 18 + 23, pixy * 18 + 11);
				Rave = GetRValue(color);
				Gave = GetGValue(color);
				Bave = GetBValue(color);
				R = Rave / 4;
				G = Gave / 4;
				B = Bave / 4;
				printf("[%d,%d] RGB(%d, %d, %d)\n", pixx, pixy, R, G, B);
			}
		}
	}
	cout << "なにか入力したら終了します" << endl;
	cin >> exit;
	return 0;
}
