
# Uso de BLAST en Linux para Buscar un Gen en un Archivo FASTA

### Paso 1: Instalar BLAST
Si no tienes **BLAST** instalado, puedes hacerlo mediante el gestor de paquetes. En sistemas **Debian/Ubuntu**, usa:

```bash
sudo apt-get install ncbi-blast+
```

### Paso 2: Preparar tus Archivos

1. **Archivo FASTA de consulta**: Asegúrate de que tu archivo FASTA contenga la secuencia del gen que deseas buscar. Por ejemplo, si tienes un archivo llamado `consulta.fasta`:

   ```
   >gen_ejemplo
   ATGCCTGAGCTAGCTAGCTAGCTAG
   ```
  Con nuestros datos 
  ```bash
  >AP2
  ATGCCTGAGCTAGCTAGCTAGCTAG...
  ```

2. **Base de datos BLAST**: Necesitarás tener una base de datos contra la que buscar. Puedes usar una base de datos existente (como la de NCBI) o crear la tuya propia a partir de un archivo FASTA.

### Paso 3: Crear una Base de Datos BLAST (si es necesario)
Si deseas crear tu propia base de datos a partir de un archivo FASTA, usa el siguiente comando:

```bash
makeblastdb -in tu_base_de_datos.fasta -dbtype nucl -out nombre_base_de_datos
```
Con nuestros datos 
*Recordar que este FASTA viene de el .bam que se convierto desde samtools con este script, este mismo se puede usar para pasar de bam a sam

```bash
samtools fasta 13_2.sam > 13_2.fasta
```

```bash
makeblastdb -in 13_2listo2.fasta -dbtype nucl -out 13_2Bas
```


- **`-in`**: Indica el archivo FASTA que usarás para crear la base de datos.
- **`-dbtype`**: Especifica el tipo de secuencia (`nucl` para secuencias nucleotídicas o `prot` para proteicas).
- **`-out`**: Especifica el nombre de la base de datos que se creará.

### Paso 4: Realizar la Búsqueda BLAST
Una vez que tengas tu archivo de consulta y tu base de datos, puedes realizar la búsqueda con el siguiente comando:

```bash
blastn -query consulta.fasta -db nombre_base_de_datos -out resultados_blast.txt -outfmt 6
```

- **`-query`**: Indica el archivo que contiene la secuencia que deseas buscar.
- **`-db`**: Especifica el nombre de la base de datos que creaste o que vas a usar.
- **`-out`**: Indica el archivo donde se guardarán los resultados de la búsqueda.
- **`-outfmt`**: Especifica el formato de salida. `6` es un formato tabular que incluye las coincidencias más relevantes.

### Paso 5: Ver los Resultados
Después de ejecutar el comando, puedes ver los resultados en el archivo `resultados_blast.txt`. Para ver el contenido directamente en la terminal, usa:

```bash
cat resultados_blast.txt
```
