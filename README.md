#define SECURE_NO_WARNINGS_
#include <stdio.h>
#include <stdlib.h>
typedef struct {
	int mes,anio;
}Tfecha;
typedef struct {
	char descripciondelproducto[32];
	int codigodebarras[21];
	int lote[5];
	float costounitario;
	int stock;
	Tfecha fechav;
} Tinfo; 

void Bajas(int *producto);
void inicializarproducto(Tinfo *elemento); //funcion con toda la informacion para un producto
int main() {
	int i;
	Tinfo producto;
	Tfecha hoy; 
	Tinfo cant[5]; //cantidad de veces que se va a inicializar la info del producto
	hoy.mes = 2; 
	hoy.anio = 2018;


	FILE *arch;
	arch = fopen("datos.dat", "wb");
	if (arch == NULL) {
		puts("No se puede abrir el archivo");
		return 1;
	}


	inicializarproducto(&producto);
	Bajas(&producto.lote);
	cant[0] = producto;
	
	


}
void Bajas(int *producto) {
	fread(&producto, sizeof(producto), 1, arch);
	while (!feof(arhc)) {
		if (producto.fechav < hoy) {
			printf("El lote se encuentra vencido");
			producto.lote = -1 * (producto.lote);
			fseek(arch, -1 * (int)sizeof(producto), seek_cur);
			fwrite(&producto, sizeof(producto), 1, arch);
			fseek(arch, 0, seek_cur);
		}
		fread(&producto, sizeof(producto), 1, arch);
	}
	fclose(arch);

}
void inicializarproducto(Tinfo *elemento) {
	strcpy(elemento->descripciondelproducto, "-");
	for (i = 0; i <= 21, i++) {
		elemento->codigodebarras = rand() % 11;
	}
	for (i = 0; i <= 5, i++) {
		elemento->lote = rand() % 999;
	}
	elemento->costounitario = rand() % 9999;
	elemento->stock = rand() % 9999; 
	elemento->fechav.mes = rand() % 12;
	elemento->fechav.anio = rand() % (2018 - 2000 + 1);

}
