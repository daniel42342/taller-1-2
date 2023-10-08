#include <stdio.h>
#include <string.h>

// Función 1 para verificar descuento de producto
int func1(char* codigoProducto) {
    char* productosConDescuento[] = {"8949899430", "7653512593", "9383867373", "88392904209"};
    int numProductos = sizeof(productosConDescuento) / sizeof(productosConDescuento[0]);
    
    for (int i = 0; i < numProductos; i++) {
        if (strcmp(codigoProducto, productosConDescuento[i]) == 0) {
            return 1; // Descuento
        }
    }
    
    return 0; // Sin descuento
}

// Función 2 para verificar participación en rifa
int func2(char* codigoProducto, char* codigoAlmacen) {
    char* codigosValidosParaRifa[] = {"894985943020763", "165331255320221", "248386737320130", "183923092220561"};
    int numCodigos = sizeof(codigosValidosParaRifa) / sizeof(codigosValidosParaRifa[0]);
    
    char codigoProductoAlmacen[20];
    snprintf(codigoProductoAlmacen, sizeof(codigoProductoAlmacen), "%s%s", codigoProducto, codigoAlmacen);
    
    for (int i = 0; i < numCodigos; i++) {
        if (strcmp(codigoProductoAlmacen, codigosValidosParaRifa[i]) == 0) {
            return 1; // Participación
        }
    }
    
    return 0; // Sin participación
}

int main() {
    char codigoProducto[11];
    char codigoAlmacen[6];
    
    // Ingresa los códigos de usuario
    printf("Código de barras del producto (10 dígitos): ");
    scanf("%s", codigoProducto);
    
    printf("Código del almacén (debe comenzar con 20): ");
    scanf("%s", codigoAlmacen);
    
    // Verificar longitudes de los códigos
    if (strlen(codigoProducto) != 10 || strlen(codigoAlmacen) != 5 || strncmp(codigoAlmacen, "20", 2) != 0) {
        printf("Error: Códigos inválidos.\n");
        return 1; // Error
    }
    
    // Verificar descuento
    if (func1(codigoProducto)) {
        printf("Tiene descuento del 20%%.\n");
    } else {
        printf("Sin descuento.\n");
    }
    
    // Verificar participación
    if (func2(codigoProducto, codigoAlmacen)) {
        printf("Puede participar en la rifa.\n");
    } else {
        printf("No puede participar en la rifa.\n");
    }
    
    return 0;
}
