# Toc-T1

Para la primera tarea del curso, la cual ha tenido que ver con el uso de la programación lineal para optimizar una serie de recursos, he llevado a cabo un análisis del problema y una reflexión sobre este en Látex, donde su respectivo pdf descargado está en el repositorio. También, orientado por el código del campus, he visto que esta técnica sí funciona y es efectiva, el cual te dejo a continuación:




# El programa de la primera tarea es el siguiente:


```

# Importamos las herramientas OR-Tools para la programacion lineal
from ortools.linear_solver import pywraplp

# Crear un solver GLOP
solver = pywraplp.Solver('Maximize army power', pywraplp.Solver.GLOP_LINEAR_PROGRAMMING)

# Crear las variables
swordsmen = solver.IntVar(0, solver.infinity(), 'swordsmen')
bowmen = solver.IntVar(0, solver.infinity(), 'bowmen')
horsemen = solver.IntVar(0, solver.infinity(), 'horsemen')

# Crear las restricciones
solver.Add(swordsmen*60 + bowmen*80 + horsemen*140 <= 1200) # Food
solver.Add(swordsmen*20 + bowmen*10 <= 800)                 # Wood
solver.Add(bowmen*40 + horsemen*100 <= 600)                 # Gold


# Crear la funcion objetivo
solver.Maximize(swordsmen*70 + bowmen*95 + horsemen*230)


# Resolver el problema
status = solver.Solve()


# Imprimir la solucion
if status == pywraplp.Solver.OPTIMAL:  
    print('================= Solución =================')  
    print(f'Resuelto en  {solver.wall_time():.2f} milisegundos en {solver.iterations()} iteraciones')  
    print(f'Poder optimizado = {solver.Objective().Value()} poder')  
    print('Ejército:');  print(f' - Espadachín = {swordsmen.solution_value()}')  
    print(f' - Arquero = {bowmen.solution_value()}')  
    print(f' - Jinete = {horsemen.solution_value()}')
else:  
    print('El solver no ha encontrado una solución óptima.')
```




