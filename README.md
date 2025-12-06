#include <iostream>
#include <fstream>
using namespace std;

class Drone {
private:
    int yuk, hiz, yukseklik, pil;

public:
    Drone(int y, int h, int ys, int p) {
        yuk = y;
        hiz = h;
        yukseklik = ys;
        pil = p;
    }

    string ucusGuvenligiKontrol() {
        if (yuk > 500)
            return "Ağır yük - Uçuş reddedildi!";
        else if (pil < 30)
            return "Pil yetersiz - Uçuş ertelendi!";
        else if (yukseklik > 200)
            return "Yükseklik sınırı aşıldı!";
        else
            return "Drone uçuşa hazır.";
    }

    void verileriKaydet(ofstream &dosya) {
        dosya << yuk << " " << hiz << " " << yukseklik << " " << pil << endl;
    }
};

int main() {
    Drone d(300, 50, 150, 80);

    cout << d.ucusGuvenligiKontrol() << endl;

    ofstream dosya("veri.txt");
    if (!dosya) {
        cout << "Dosya açılamadı!" << endl;
        return 1;
    }

    d.verileriKaydet(dosya);
    dosya.close();

    cout << "Veriler dosyaya yazıldı." << endl;
    return 0;
}
