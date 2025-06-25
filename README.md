estado = True
compradoresregis = {} 
entradas1 = 50
entradas2 = 60
stockini1 = entradas1
stockini2 = entradas2

while estado:
    try:
        print("\n***SHOW DE HIPHOP***")
        print("Bienvenido al sistema de venta de entradas del Concierto de Movimiento original")
        print("1. Comprar entradas")
        print("2. Cambiar show")
        print("3. Mostrar stock de funciones")
        print("4. Salir")
        opcion = int(input('Seleccione una opción (1-4): '))
        while opcion < 1 or opcion > 4:
            print('Error, intente nuevamente. Solo opciones del 1 al 4.') 
            opcion = int(input('Seleccione una opción (1-4): '))

        if opcion == 1:
            print('---Comprar entradas---')
            nombrepersona = input('Ingrese el nombre del comprador: ').strip()
            if nombrepersona in compradoresregis:
                print(f'Error: El comprador {nombrepersona} ya tiene una entrada registrada')
                continue
            
            print('---Seleccione el show---')
            print('1. Movimiento Original con los Shamanes Crew')
            print('2. Movimiento Original con Chyste MC')
            eleccion = int(input('Seleccione el show a comprar (1 o 2): '))

            while eleccion not in [1, 2]:
                print('Error: Selección de show inválida. Favor de ingresar solo opción 1 o 2.')
                eleccion = int(input('Seleccione el show a comprar (1 o 2): '))
            
            if eleccion == 1:
                if entradas1 > 0:
                    entradas1 -= 1
                    compradoresregis[nombrepersona] = 1 
                    print(f'Se ha realizado la compra de {nombrepersona} con éxito')
                else: 
                    print('Lo sentimos, no quedan entradas disponibles para Movimiento con los Shamanes Crew')

            elif eleccion == 2:
                if entradas2 > 0:
                    entradas2 -= 1
                    
                    compradoresregis[nombrepersona] = 2
                    print(f'Se ha realizado la compra de {nombrepersona} con éxito')
                else: 
                    print('Lo sentimos, no quedan entradas disponibles para Movimiento con Chyste MC')
        
        
        elif opcion == 2:
            print('---Cambiar Show---')
            nombrecambio = input('Ingrese el nombre del comprador que desea cambiar de show: ').strip()
            
            if nombrecambio in compradoresregis:
                
                showactual = compradoresregis[nombrecambio]
                
                show1_nombre = "Movimiento Original con los Shamanes Crew"
                show2_nombre = "Movimiento Original con Chyste MC"

                if showactual == 1:
                    showdestino = 2
                    show_actual_nombre = show1_nombre
                    show_destino_nombre = show2_nombre 
                else:
                    showdestino = 1
                    show_actual_nombre = show2_nombre
                    show_destino_nombre = show1_nombre

                print(f'{nombrecambio} tiene una entrada para: {show_actual_nombre}.')
                confirmar = input(f'¿Desea cambiar a la función "{show_destino_nombre}"? (s/n): ').strip().lower()
            
                if confirmar == 's':
                    if showdestino == 1 and entradas1 > 0:
                        entradas1 -= 1
                        entradas2 += 1
                        compradoresregis[nombrecambio] = 1
                        print(f'Cambio realizado con éxito. {nombrecambio} ahora tiene entrada para {show_destino_nombre}.')
                    elif showdestino == 2 and entradas2 > 0:
                        entradas2 -= 1
                        entradas1 += 1
                        compradoresregis[nombrecambio] = 2
                        print(f'Cambio realizado con éxito. {nombrecambio} ahora tiene entrada para {show_destino_nombre}.')
                    else:
                        
                        print(f'Lo sentimos, no quedan entradas disponibles para cambiar a la función "{show_destino_nombre}".')
                else:
                    print('Operación de cambio cancelada.')
            else:
                print(f'Error: El comprador "{nombrecambio}" no se encuentra registrado.')

        elif opcion == 3:
            print('---Resumen y Totales de Entradas---')
            vendidas1 = stockini1 - entradas1
            vendidas2 = stockini2 - entradas2
            total_disponible = entradas1 + entradas2
            total_vendido = vendidas1 + vendidas2
            total_general = stockini1 + stockini2

            print("--- Detalle por Show ---")
            print(f"1. Movimiento Original con los Shamanes Crew:")
            print(f" -- Disponibles: {entradas1} -- Vendidas: {vendidas1} -- Capacidad Total: {stockini1} -- ")
            
            print(f"2. Movimiento Original con Chyste MC:")
            print(f" -- Disponibles: {entradas2} -- Vendidas: {vendidas2} -- Capacidad Total: {stockini2} -- ")
            
            print("---Totales Generales---")
            print(f"Total de Entradas Disponibles (ambos shows): {total_disponible}")
            print(f"Total de Entradas Vendidas (ambos shows): {total_vendido}")
            print(f"Capacidad Total del Evento (ambos shows): {total_general}")
            
            if compradoresregis:
                print("--- Compradores Registrados---")
                for comprador, show in compradoresregis.items():
                    show_nombre = "Movimiento Original con los Shamanes Crew" if show == 1 else "Movimiento Original con Chyste MC"
                    print(f" {comprador} (Show: {show_nombre})")
            else:
                print("No hay compradores registrados.")

        elif opcion == 4:
            print('Saliendo del sistema, ¡gracias por usar nuestros servicios!')
            estado = False
            
    except ValueError:
        print('Error: Ingrese solo un valor numérico para las opciones.')
