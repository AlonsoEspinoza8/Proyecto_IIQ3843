<<<<<<< HEAD
# Proyecto_IIQ3843

Repositorio creado para publicar avances del proyecto.

Avances 29/10: Creación de repositorio y verificación de la instalación de la librería ```CryoEvap```
=======
# Proyecto: Simulación de transferencia de calor transiente durante la carga y descarga de amoníaco verde refrigerado en tanques cilíndricos verticalmente orientados.

## Carga de amoníaco

Para simular la carga de amoníaco, se realizan balances de masa y energía, además de un análisis de la transferencia de calor sobre el vapor presente en el tanque.

![alt text](<Archivos Charla Relámpago/Diagrama_carga.png>)

**Definiciones**

- $\dot{m}_{L}$: Flujo másico de entrada al estanque $[kg/s]$.
- $\dot{B}_{L}$: Tasa de evaporación de líquido $[kg/s]$.
- $\dot{B}$: Tasa de *Boil-off gas* $[kg/s]$.
- $\dot{Q}_{L} = U_L A_L (T_{air} - T_L)$: Ingreso de calor desde el exterior hacia la fase líquida $[W]$.
- $\dot{Q}_{V} = U_V (1 - \eta_W) A_V (T_{air} - \overline{T}_v)$: Ingreso de calor desde el exterior hacia la fase de vapor $[W]$
- $\dot{Q}_{b}$: Ingreso de calor desde el fonde del tanque debido a una fuente externa $[W]$.
- $\dot{Q}_{VL} = \frac{\pi d_i^2}{4} \overline{k}_v \frac{\partial T}{\partial z}|_{z = 0}$: Ingreso de calor hacia el líquido debido al vapor sobrecalentado mediante conducción $[W]$.
- $\dot{Q}_{V,w} = \eta_w \dot{Q}_{V}$: Calor del exterior dirigido hacia el vapor que es conducido hacia la interfaz líquido vapor $[W]$.

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

- Se modifica la clase ```Tank``` del archivo ```CryoEvap/cryoevap/storage_tanks/tank.py``` en el método ```sys_liq_volume```. Ahora, en vez de retornar ```-1 / self.cryogen.rho_L * (Q_L_tot/dH_LV)``` (tasa de cambio del volumen del líquido en ausencia de flujo másico de entrada), retorna ```-1 / self.cryogen.rho_L * (Q_L_tot/dH_LV) + (self.m_L / self.cryogen.rho_L)``` (la tasa de cambio del volumen actualizada)
