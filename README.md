# Expendedora-C-
## Nombre: Valeria Curiel Colin
### Clase: Tecnicaas de Programacion
#### Profesor: Jorge Armando Rodriguez Vera 
### Mecatrónica Gpo 2
Este repo guarda las versiones del proyecto Expendedora para la clase de Tecnicas de Programación de la FI UNAM

Para ejecutar, abra el .cs

[Si se desea acceder en linea: CLIC AQUI ](https://drive.google.com/drive/folders/1I8G0kgHNQ8lHXvzV927EsnekVdfQVyTq?usp=drive_link ).
![imagen exp](https://d379p6s0o40qsz.cloudfront.net/2023-07/Maquina_Combo_Frente.png?VersionId=FZauAqTQoP7biALm4Q78.6CwzouiYZaY)


##CÓDIGO
```
using System;
using System.Threading;


namespace Expendedoras
{
    public abstract class Expendedora //clase publica
    {
        #region Atributos
        private string _marca;
        private sbyte _temperatura;
        private ushort _cantProductos;
        private float _precio;


            #region Props o encapsuado
            //encapsulamiento de temperatura, value toma el valor de _temperatura, usado para proteccion
            public sbyte Temperatura 
            { 
                get => _temperatura;
                set
                {
                    if (value >= 10 && value < 20)
                    {
                        _temperatura = value; //temp correcta
                    }
                    else
                    {
                        _temperatura = 18;
                    }
                }


            }

            public string Marca { get => _marca; set => _marca = value; }
            #endregion

        #endregion

        #region Constructores
        //constructor

        public Expendedora()
        {
            //Aqui iniciamos atributos si queremos cambiar el valor default
            Temperatura = 25;
            _precio = 15;
            Marca = "AWS\n"; //Defini el atributo hasta el constructor
            //EN EL CONSTRUCTOR LLAMAMOS A LOS MÉTODOS
            Saludar();
            Thread.Sleep(3000); //milisegs ESPERA PARA CAMBIAR PANTALLA 
            //Console.Clear();
            string Codigo = MostrarProducto();
            ClearDisplay();
            MostrarPrecio(Codigo); // Codigo en expendedora es diferente de codigo en Mostrar precio

            //UNA VARIABLE LOCAL es NECESARIO INICIALIZARLA
        }
        public Expendedora(bool mantenimiento ) //no problema pq recibe parametro
        {
            if (mantenimiento)
            {
                Console.WriteLine("Hola, ingresa nueva temperatura");
                Temperatura = sbyte.Parse(Console.ReadLine());
                ClearDisplay();
                Console.WriteLine("Temperatura: {0} °C", Temperatura);
            }
        }

        #endregion

        #region METoDOS
        public void ClearDisplay()
        {
            Thread.Sleep(1000); 
            Console.Clear();
        }
        //metodo
        public void Saludar()
        {
            Console.WriteLine("{0}Bienvenido, elige tu producton\nTemperatura: {1}°", Marca, Temperatura);
        }       
        public string MostrarProducto()
        {
            string codigo; // Variable local, no requiere de un modificador de acceso porque requiere del
                           // métdo donde se encuentra
            Console.WriteLine("2A: Papas, \t3C: Chocolate");
            Console.WriteLine("INGRESA EL CODIGO DEL PRODUCTO");
            codigo = Console.ReadLine();
            return codigo;
        }
        public void MostrarPrecio(string codigo)
        {
            //
            switch(codigo)
            {
                case "2A":
                    Console.WriteLine("Precio: ${0}", _precio); //Vale 0 y ahora 15
                    break;
                case "3C":
                    Console.WriteLine("Precio: ${0}", _precio+=5); //reasigna valor a _precio
                    break;
                default:
                    Console.WriteLine("Producto no encontrado");
                    break;
            }
          
        }
        #endregion

    }
}
```
