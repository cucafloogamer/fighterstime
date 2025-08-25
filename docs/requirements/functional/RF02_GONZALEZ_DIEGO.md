# SISTEMA DE COMBATE
El combate tendrá un tiempo limite de 180s (3 minutos) 
El daño será calculado de manera tal que la defensa de el personaje que recibe el ataque sea afectada antes que la vida de total del jugador.
por lo tanto si un personaje tiene 10 de defensa y el atacante le hace 7 de daño esta defensa pasa a ser 3, lo cual lo deja mucho más serca de recibir daño total.
si recibe un daño mayor a la defensa base del personaje, se le aplicara el dato restante a la vida total de quien recibio el ataque, Por Ejemplo, si un jugador tiene 10 de defensa y recibe 11 de daño, pierde su defensa total, dejandolo expuesto y recibiendo 1 de daño total en la vida del jugador siendo atacado.


![EjemploFormuladeDaño](/docs/assets/damage.png)

Daño = (AtaqueBase-DefensaBase)*tipoAtaque*Tipo+item

