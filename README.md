# 基於LLaMA-7B y LoRA 之醫學數據問答集
Conjunto de preguntas y respuestas de datos médicos basado en LLaMA-7B y LoRA Este proyecto tiene como objetivo utilizar el modelo LLaMA-7B y aplicarlo a preguntas y respuestas de datos médicos a través del método de ajuste fino de LoRA. Utilizamos el conjunto de datos PubMedQ&A para la capacitación

Cómo usarlo: primero descargue los paquetes dependientes enumerados en require.txt: pip install -r require.txt. Después de instalar el paquete, ejecute el siguiente comando: python app.py para ingresar a la interfaz de prueba real. Solo necesita ingresar la instrucción y la entrada para obtener la salida correspondiente. Nota: Confirme que su dispositivo GPU tenga suficiente vRAM. Este proyecto fue desarrollado usando nVidia 2070×2. Cómo ajustar el modelo. Si desea ajustar el modelo, abra llama.ipynb. Primero, asegúrese de que el conjunto de datos tenga el formato ['instrucción', 'entrada', 'salida']. Entre ellos, la parte de entrada puede estar vacía. A continuación, se pueden ajustar los siguientes parámetros:

MICRO_BATCH_SIZE = 4    
BATCH_SIZE = 128
GRADIENT_ACCUMULATION_STEPS = BATCH_SIZE // MICRO_BATCH_SIZE
EPOCHS = 3  
LEARNING_RATE = 3e-4  
CUTOFF_LEN = 128  
LORA_R = 8
LORA_ALPHA = 16
LORA_DROPOUT = 0.05
VAL_SET_SIZE=10
```
Estos parámetros se pueden ajustar según sus propias necesidades y equipos de hardware. En nuestros experimentos, se utilizó un conjunto de datos de 211.300 registros y el entrenamiento tomó aproximadamente 8 horas en una GPU con nVidia 2070×2.

## Cómo utilizar el modelo entrenado
Cuando se completa la capacitación, los archivos del modelo almacenados se pueden encontrar en la carpeta especificada. Los nombres de los archivos deben ser `adapter_model.bin` y `adapter_config.json`. En nuestros experimentos, guardamos estos archivos de modelo en una carpeta llamada `lora-alpaca-1000`. Puede consultar nuestros archivos de modelo entrenados y sus formatos relacionados en esta carpeta. A continuación, debe editar `app.py`, apuntar el parámetro `lora_weights` a la ruta de la carpeta donde está almacenado el modelo y luego ejecutar el programa.
