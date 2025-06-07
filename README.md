# Informe-de-Gestion-por-locales
Se informa a cliente de la gestion de 4 locales 
# 📊 Análisis de Rentabilidad de Tiendas

Este repositorio contiene un análisis en Python para comparar el desempeño de **cuatro tiendas** en base a sus métricas de ventas (ingresos), costos de envío promedio de los productos, calificacion de la tienda por parte de los clientes  y categoria y productos (mas/menos) vendidos.
Se define la peor tienda aplicando la metrica de rentabilidad promedio por tienda. Esto a su vez es el resultado de los ingresos - (costo promedio de envio * cantidad de productos vendidos)
Se concluye que la tenda 4 es la que presenta la menor rentabilidad

---

## 📁 Archivos

- `tienda_1.csv`, `tienda_2.csv`, `tienda_3.csv`, `tienda_4.csv`: Datos de productos vendidos por tienda.
- `main.py`: Script de Python con el análisis.
- `grafico_radar.png`, `grafico_burbuja.png` y grafico de barras: Visualizaciones generadas.

---

## 📈 Métricas Calculadas

Para cada tienda, se calcularon las siguientes métricas:

- **Ingresos totales**: Suma de los precios de todos los productos vendidos.
- **Productos vendidos**: Cantidad total de registros por tienda.
- **Costo de envío promedio**: Promedio de la columna `Costo Envío`.
- ** Reseñas de los clientes** . Calificaciones de los clientes por tiendas.
- **Categorias de productos mas vendidos**.
- **Rentabilidad neta**: Ingresos totales - (Costo promedio de envío × cantidad de productos).

---

## 🧮 Código principal

```python
def calcular_metricas(df):
    ingresos = df["Precio"].sum()
    productos = len(df)
    costo_envio = df["Costo Envío"].mean()
    rentabilidad_neta = ingresos - (costo_envio * productos)
    return ingresos, productos, costo_envio, rentabilidad_neta

# Resultados por tienda
resultados = {
    "Tienda 1": calcular_metricas(tienda1),
    "Tienda 2": calcular_metricas(tienda2),
    "Tienda 3": calcular_metricas(tienda3),
    "Tienda 4": calcular_metricas(tienda4),
}

df_resultados = pd.DataFrame(resultados, index=["Ingresos", "Productos Vendidos", "Costo Envío Promedio", "Rentabilidad Neta"]).T
print(df_resultados)

# Tienda más y menos rentable
tienda_mas_rentable = df_resultados["Rentabilidad Neta"].idxmax()
tienda_menos_rentable = df_resultados["Rentabilidad Neta"].idxmin()

print(f"🟢 Tienda más rentable: {tienda_mas_rentable}")
print(f"🔴 Tienda menos rentable: {tienda_menos_rentable}")
