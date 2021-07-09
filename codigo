#Importamos punciones de la libreria pulp
from pulp import LpProblem, LpVariable, LpStatus, LpMinimize, GLPK, value

#Datos para optimizar el problema
m = 3 # Puntos de oferta
m = 3 # Puntos de demanda
a = range(1, M + 1)
a1 = range(M)
b = range(1, N+1)
b1 = range(N)

#lista de variables para x
xindx = [(a[i] , b[j]) for j in b1 for i in a1]

#creacion del modelo que contendrá los datos y resuelve
modelo = LpProblem("problema del transporte", LpMinimize)

#creacion de las variables de desicion
x = LpVariable.dicts("X", xindx, 0, None)

#funcion objetivo del problema
modelo += 4.0 * x[1,1] + 3.0 * x[1,2] + 8.0 * x[1,3] \
+ 7.0 * x[2,1] + 5.0 * x[2,2] + 9.0 * x[2,3] \
+ 4.0 * x[3,1] + 5.0 * x[3,2] + 5.0 * x[3,3],"costo de transporte"

#restricciones de oferta
modelo += x[1,1] + x[1,2] + x[1,3] <= 300.0, "oferta parte 1"
modelo += x[2,1] + x[2,2] + x[2,3] <= 300.0, "oferta parte 2"
modelo += x[3,1] + x[3,2] + x[3,3] <= 100.0, "oferta parte 3"

#restricciones de demanda
modelo += x[1,1] + x[2,1] + x[3,1] >= 200.0, "demanda parte 1"
modelo += x[1,2] + x[2,2] + x[3,2] >= 200.0, "demanda parte 2"
modelo += x[1,3] + x[2,3] + x[3,3] >= 300.0, "demanda parte 3"

#usamos el problema utilizando el pulp solver
modelo.solve(GLPK())

#imprimo el estado de la solucion
print("estado:", LpStatus[modelo.status])

#imprimimos cada una de las variables con que se resolvió el \
#valor optimo
for v in modelo.varibales():
    print(v.name, "=", v.varValue)

#imprimimos el valor optimizado de la funcion objetivo
print("funcion objetivo", value(modelo.objective))
