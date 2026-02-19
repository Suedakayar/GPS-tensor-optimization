#include <stdio.h>
#include <stdlib.h>
#include <stdint.h>
#include <math.h>


typedef enum { T_FLOAT32, T_INT8 } TensorModu;

typedef struct {
    TensorModu mod;
    uint32_t veri_sayisi;
    float olcek;

    union {
        float* f_mesafe_ptr;
        int8_t* i_sikismis_ptr;
    } bellek;
} MesafeTensor;


int8_t mesafe_sikistir(float km, float scale) {

    return (int8_t)round(km / scale);
}


float mesafe_coz(int8_t q_km, float scale) {
    return (float)q_km * scale;
}


int main() {
    MesafeTensor kosuTensor;
    kosuTensor.veri_sayisi = 1;
    kosuTensor.olcek = 0.2f;


    kosuTensor.bellek.i_sikismis_ptr = (int8_t*)malloc(sizeof(int8_t));

    float anlik_km;

    printf("=== AKILLI KOSU TAKIP VE MESAFE TENSORU ===\n");
    printf("Hocam, GPS verileri alinmaya baslandi...\n\n");

    while(1) {
        printf("Katedilen Mesafeyi Girin (Orn: 5.42 veya 12.87) [Durmak icin 0]: ");


        if (scanf("%f", &anlik_km) != 1 || anlik_km == 0) break;


        kosuTensor.bellek.i_sikismis_ptr[0] = mesafe_sikistir(anlik_km, kosuTensor.olcek);


        int8_t saklanan_veri = kosuTensor.bellek.i_sikismis_ptr[0];
        float geri_cozulen = mesafe_coz(saklanan_veri, kosuTensor.olcek);


        printf("\n--- GPS VERI ANALIZI ---\n");
        printf("GPS'ten Gelen: %.2f KM (32-bit Float)\n", anlik_km);
        printf("Tensorde Saklanan: %d (8-bit Integer - 1 Byte)\n", saklanan_veri);
        printf("Sistemin Okudugu: %.2f KM\n", geri_cozulen);
        printf("Hata Payi: %.2f KM | Bellek Tasarrufu: %%75\n", fabs(anlik_km - geri_cozulen));
        printf("-------------------------------------------\n\n");
    }

    free(kosuTensor.bellek.i_sikismis_ptr);
    return 0;
