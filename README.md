# Función para ingresar productos y precios en una tienda
def ingresar_productos(tienda):
    productos = []
    print(f"Ingresar productos para la {tienda}:")
    while True:
        producto = input("Ingrese el nombre del producto (o 'fin' para terminar): ")
        if producto.lower() == 'fin':
            break
        precio = float(input(f"Ingrese el precio del producto {producto}: "))
        productos.append((producto, precio))
    return productos

# Función para comparar precios de productos entre dos tiendas
def comparar_precios(productos_tienda1, productos_tienda2):
    resumen_comparativo = []
    
    for producto1 in productos_tienda1:
        for producto2 in productos_tienda2:
            if producto1[0] == producto2[0]:
                mejor_precio = producto1 if producto1[1] < producto2[1] else producto2
                tienda_mejor_precio = "Tienda 1" if mejor_precio == producto1 else "Tienda 2"
                resumen_comparativo.append(
                    f"Producto: {producto1[0]} - Mejor precio: {mejor_precio[1]} en {tienda_mejor_precio}"
                )
    return resumen_comparativo

# Función para calcular el total y el promedio de los precios de una tienda
def calcular_operaciones(productos):
    total = sum(precio for producto, precio in productos)  # Sumar los precios de todos los productos
    promedio = total / len(productos) if productos else 0  # Promedio de precios
    return total, promedio

# Función para guardar el análisis comparativo en un archivo
def guardar_analisis_comparativo(analisis, archivo_salida):
    with open(archivo_salida, 'w') as file:
        for linea in analisis:
            file.write(linea + '\n')

# Función para guardar las operaciones aritméticas (total y promedio) en un archivo
def guardar_operaciones(total, promedio, archivo_salida):
    with open(archivo_salida, 'w') as file:
        file.write(f"Total de los precios: {total}\n")
        file.write(f"Promedio de los precios: {promedio}\n")

# Función principal donde se ejecutan las tareas
def main():
    # Ingresar productos y precios en dos tiendas
    productos_tienda1 = ingresar_productos("Tienda 1")
    productos_tienda2 = ingresar_productos("Tienda 2")
    
    # Comparar los precios entre las dos tiendas
    analisis_comparativo = comparar_precios(productos_tienda1, productos_tienda2)
    
    # Mostrar el resumen comparativo
    print("\nAnálisis de precios entre las dos tiendas:")
    for linea in analisis_comparativo:
        print(linea)
    
    # Guardar el análisis comparativo en un archivo
    archivo_salida_comparativo = "analisis_comparativo_productos_electronicos.txt"
    guardar_analisis_comparativo(analisis_comparativo, archivo_salida_comparativo)
    print(f"\nEl análisis comparativo ha sido guardado en el archivo: {archivo_salida_comparativo}")
    
    # Realizar operaciones sobre los precios
    total_tienda1, promedio_tienda1 = calcular_operaciones(productos_tienda1)
    total_tienda2, promedio_tienda2 = calcular_operaciones(productos_tienda2)
    
    # Guardar las operaciones en un archivo
    archivo_salida_operaciones = "operaciones.txt"
    guardar_operaciones(total_tienda1, promedio_tienda1, archivo_salida_operaciones)
    print(f"\nLas operaciones aritméticas han sido guardadas en el archivo: {archivo_salida_operaciones}")
    
    # Copiar todo el contenido a otro archivo final
    archivo_final = "resultado.txt"
    with open(archivo_final, 'w') as file:
        file.write(f"Análisis comparativo de precios:\n")
        for linea in analisis_comparativo:
            file.write(linea + '\n')
        file.write(f"\nOperaciones de precios:\n")
        file.write(f"Total Tienda 1: {total_tienda1}, Promedio Tienda 1: {promedio_tienda1}\n")
        file.write(f"Total Tienda 2: {total_tienda2}, Promedio Tienda 2: {promedio_tienda2}\n")
    
    print(f"\nEl contenido final ha sido guardado en el archivo: {archivo_final}")

# Ejecutar el programa
if __name__ == "__main__":
    main()

