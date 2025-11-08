<<<<<<< HEAD
# Proyecto_IIQ3843

Repositorio creado para publicar avances del proyecto.

Avances 29/10: Creación de repositorio y verificación de la instalación de la librería ```CryoEvap```
=======
# Proyecto: Simulación de transferencia de calor transiente durante la carga y descarga de amoníaco verde refrigerado en tanques cilíndricos verticalmente orientados.

## Carga de amoníaco

Para simular la carga de amoníaco, se realizan balances de masa y energía, además de un análisis de la transferencia de calor sobre el vapor presente en el tanque.

**Balance de masa en el líquido del tanque**

$$
\frac{d}{dt}(\rho_L V_L) = \dot{m}_L - \dot{B}_L
$$

**Balance de energía en el líquido del tanque**

$$
\dot{Q}_{bottom} + \dot{Q}_{L} + \dot{Q}_{V,w} + \dot{Q}_{VL} + \dot{m}_L h_L - \dot{B}_L h_v = \frac{d}{dt}(\rho_L V_L h_L)
$$

Reemplazando la ecuación del balance de masa en el balance de energía, y considerando que en un proceso isobárico tanto la presión como la entalpía son constantes, se tiene:

$$
\dot{Q}_{bottom} + \dot{Q}_{L} + \dot{Q}_{V,w} + \dot{Q}_{VL} + \dot{m}_L h_L - \dot{B}_L h_v = h_L (\dot{m}_L - \dot{B}_L)
$$

$$
\dot{Q}_{bottom} + \dot{Q}_{L} + \dot{Q}_{V,w} + \dot{Q}_{VL} + - \dot{B}_L h_v = - \dot{B}_L h_L
$$

$$
\dot{B}_L = \frac{\dot{Q}_{bottom} + \dot{Q}_{L} + \dot{Q}_{V,w} + \dot{Q}_{VL}}{h_v - h_L}
$$

Así, de esta forma se vuelve a reemplazar en el balance de masas y se obtiene:

$$
\frac{dV_L}{dt} = \frac{\dot{m}_L}{\rho_L} - \frac{\dot{Q}_{bottom} + \dot{Q}_{L} + \dot{Q}_{V,w} + \dot{Q}_{VL}}{\rho_L(h_v - h_L)}
$$

**Modificación en el código**

- Se modifica el método ```__init__``` de la clase ```Tank``` del archivo ```CryoEvap/cryoevap/storage_tanks/tank.py```. Ahora, tiene como argumento el flujo másico de entrada $\dot{m}_{L}$.

- Se modifica la clase ```Tank``` del archivo ```CryoEvap/cryoevap/storage_tanks/tank.py``` en el método ```sys_liq_volume```. Ahora, en vez de retornar 
>>>>>>> 95382f2 (Cambios viernes 07/11)
