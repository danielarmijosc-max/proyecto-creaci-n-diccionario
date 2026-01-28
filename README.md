# proyecto-creaci-n-diccionario
Contiene programación para generar la posible contraseña del proyecto



#!/bin/bash

# Limpiar salida anterior
> diccionario.txt

while read nombre; do
  while read num; do

    # 1. nombre + numero y numero + nombre
    combos=(
      "${nombre}${num}"
      "${num}${nombre}"
    )

    # 2. numero dentro del nombre
    for ((i=0; i<=${#nombre}; i++)); do
      combos+=("${nombre:0:i}${num}${nombre:i}")
    done

    # 3. nombre dentro del numero
    for ((j=0; j<=${#num}; j++)); do
      combos+=("${num:0:j}${nombre}${num:j}")
    done

    # 4. Variaciones de mayusculas/minusculas
    for palabra in "${combos[@]}"; do
      echo "${palabra,,}" >> diccionario.txt          # minusculas
      echo "${palabra^^}" >> diccionario.txt          # MAYUSCULAS
      echo "${palabra^}"  >> diccionario.txt          # Capitalizada
    done

  done < anios.txt
done < nombres.txt

# Eliminar duplicados
sort -u diccionario.txt -o diccionario.txt
