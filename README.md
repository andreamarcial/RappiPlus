# RappiPlus
De datos a decisiones de negocio 
### **Introducción**

RappiPlus es un servicio de suscripción dentro del ecosistema de Rappi diseñado para aumentar la frecuencia de compra y el valor generado por usuario.

Sin embargo, el equipo de negocio no tiene claro si el servicio está cumpliendo su objetivo.

Existen dudas clave:

- ¿Los usuarios realmente compran más?
- ¿El modelo está generando ganancias?
- ¿Se están perdiendo oportunidades en el proceso de compra?

Para responder estas preguntas, trabajarás con datos de pedidos, catálogo y marketing.

Tu análisis permitirá entender el desempeño del servicio y detectar oportunidades concretas de mejora.

---

# **🎯 Objetivo del proyecto**

A lo largo de este proyecto responderás:

- ¿Podemos confiar en los datos?
- ¿Estamos ganando dinero?
- ¿Dónde se pierden los usuarios?
- ¿Los usuarios regresan?
- ¿Los cambios generan impacto?
- ¿Cómo comunicamos todo esto?

---

# **🔄 Que se espera en cada paso**

| **Pasos** | **Pregunta clave** | **Resultado esperado** |
| --- | --- | --- |
| 1 | ¿Podemos confiar en los datos? | Dataset limpio |
| 2 | ¿El negocio es rentable? | KPIS(Revenue, cost, profit) |
| 3 | ¿Dónde se pierden usuarios? | Funnel |
| 4 | ¿Los usuarios regresan? | Cohortes |
| 5 | ¿Los cambios funcionan? | Test estadístico |
| 6 | ¿Cómo comunicamos? | Dashboard |


---
## KPI´S DE RENTABILIDAD
 Ingreso total (Revenue):      $9,610,018.94
 Costo total:                  $3,828,869.01
 Ganancia Bruta:               $5,781,149.93
 Inversión en marketing:       $2,871,843.53
 Profit:                       $2,909,306.40
 Margen de profit:             30.27%
 
 ## Punto de atención: 
El gasto en marketing de **\$2.87 M** está muy cerca del Profit de  **\$2.9 M** — si la inversión en marketing sube un poco, el negocio podría volverse no rentable. Vale la pena analizar el ROI por canal.

      canal   ingresos     gasto    ROI
paid_search 3209280.07 922374.20 247.94
     social 3222510.32 976818.37 229.90
    organic 3178228.55 972650.96 226.76
    
Los tres canales son muy **Rentales** con un ROI de más del 200%, existe un campaña de marketing balanceada.

 categoria_producto   ingresos  costo_total  ordenes     profit  margen_pct
             Hogar 3232626.44   1213436.96     8346 2019189.48       62.46
              Moda 3172662.10   1290543.48     8295 1882118.62       59.32
       Electronica 3204730.40   1324888.57     8265 1879841.83       58.66
       
Hogar es la categoría con mejor margen y mayor *profit* 

 pais   ingresos  ordenes  ticket_promedio  ingresos_pct
   Mexico 3207047.74     8308       386.019227         33.37
 Colombia 3170333.82     8280       382.890558         32.99
Argentina 3120649.33     8022       389.011385         32.47
  Unknown  111988.05      296       378.338007          1.17
  
Los tres paises están bastante equilibrados lo que habla de una expanción regional muy balanceada. **Argentina** tiene un ticket promedio más alto, sus clientes gastan más por orden, aunque tienen menos órdenes en total.

## **📌 Petición del jefe**

> “Quiero entender en qué parte del proceso los usuarios dejan de comprar.”
> 
El mayor punto de fuga es add_payment_info — aquí se pierden 958 usuarios (13.29%) respecto a begin_checkout. Posibles causas:
- Proceso de pago largo o complicado
- Falta de métodos de pago preferidos
- Desconfianza al ingresar datos bancarios

Hay una anomalía ya que `add_to_cart` presenta más usaurios que el paso anterior `select_item`, lo que indica que hay usuarios que agregan al carrito sin haber seleccionado productos.
---

### **📌 Petición del jefe**

“Necesito saber si los usuarios regresan o abandonan la plataforma.”

---
<img width="600" height="455" alt="image" src="https://github.com/user-attachments/assets/eee8e542-0c3f-487f-a980-f2cabc7cd0b0" />

## OBSERVACIONES
La retención crece con el tiempo — el patrón es inusual pero positivo: más usuarios están activos en semana 3 que en semana 1. Esto sugiere que los usuarios tardan en "activarse" pero una vez enganchados, siguen usando la plataforma.
La cohorte de febrero es la mejor, por lo que vale la pena analizar si se realizó alguna campaña especial ese mes. 


<img width="595" height="420" alt="image" src="https://github.com/user-attachments/assets/381250b7-5f77-4d5c-9c5a-2b79aba9d94f" />


## OBSERVACIONES
Se muestra el mismo patrón de retención en los países con la mejor retención en la semana 3 y siendo febrero la mejor Cohorte.


---

### **📌 Petición del jefe**

“Hemos hecho cambios en el producto, necesito saber si realmente tuvieron impacto.”

---
==================================================
RESULTADOS DEL EXPERIMENTO A/B
==================================================
Tasa conversión control:     0.1569 (15.69%)
Tasa conversión tratamiento: 0.1629 (16.29%)
Diferencia absoluta:         0.0060 (0.60 puntos porcentuales)
Mejora relativa:             3.80%

==================================================
DECISIÓN ESTADÍSTICA (α = 0.05)
==================================================

 p-value (0.4161) ≥ α (0.05)

--------------------------------------------------
→ NO RECHAZAMOS H₀: No hay diferencia significativa
→ RECOMENDACIÓN: NO implementar el cambio
  La diferencia observada puede deberse al azar

  ## OBSERVACIONES
La diferencia que observas entre los grupos podría perfectamente deberse a la variabilidad natural de los datos, no a un efecto real del nuevo checkout UI.

**Analizaremos que debemos cambiar en nuestro experimento para observar algún cambio**
============================================================
ANÁLISIS DE PODER ESTADÍSTICO
============================================================
Tasa de conversión control:    0.1569 (15.69%)
Tasa de conversión tratamiento: 0.1629 (16.29%)
Diferencia observada:          0.0060 (0.60 puntos porcentuales)
Tamaño del efecto (Cohen's h): -0.0164
Tamaño de muestra por grupo:   ~5000
Nivel de significancia (α):    0.05

 PODER ESTADÍSTICO ESTIMADO: 0.1296 (13.0%)
 PODER INSUFICIENTE: El experimento tiene bajo poder para detectar esta diferencia
 Esto explica por qué no se encontró significancia estadística

 **El experimento actual estaba "subdimensionado":**

- Se necesitabas más usuarios (58,575 vs 5,000 por grupo)
Esto explica perfectamente por qué no se encontró significancia estadística

- Para detectar una mejora del 6.4% → 21,299 usuarios/grupo
- Para detectar una mejora del 12.7% → 5,456 usuarios/grupo (similar a la muestra actual)

---

### **📌 Petición del jefe**

“Necesito una forma clara y rápida de entender todo el análisis.”


  <img width="1445" height="800" alt="image" src="https://github.com/user-attachments/assets/bb84cb3e-97e7-49ef-9de5-0759099202b2" />

<img width="1487" height="840" alt="image" src="https://github.com/user-attachments/assets/9b55bab4-fcc0-40ab-bfb8-f42e513c1b8c" />
