using System;
using System.Collections;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace Attar_Nahuel_Parcial_1
{


    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();

        }

        ArrayList reservas = new ArrayList();

        public class Habitacion
        {
            public string NumeroHabitacion;
            public string Huesped;
            public int Cantidadnoches;



        }
        public class habitacionSimple : Habitacion
        {

        }
        public class habitacionDoble : Habitacion
        {
            public bool Tienebalcon;
        }

        private void button1_Click(object sender, EventArgs e)
        {
            textBox3.Enabled = false;
            textBox1.Enabled = false;
            textBox2.Enabled = false;
            groupBox1.Enabled = false;

            if (comboBox1.SelectedIndex == -1)
            {
                MessageBox.Show($"debe seleccionar un tipo de habitacion ");
                return;
            }


            if (string.IsNullOrEmpty(textBox1.Text.Trim()))
            {
                MessageBox.Show($"error: elija un numero de habitacion ");
                return;
            }
            if (string.IsNullOrEmpty(textBox2.Text.Trim()))
            {
                MessageBox.Show($"ingrese un huesped ");
                return;
            }
            if (string.IsNullOrEmpty(textBox3.Text.Trim()) || !int.TryParse(textBox3.Text, out int noche) || noche < 1)
            {
                MessageBox.Show($"ingrese la cantidad de noches ");
                return;
            }


            if (comboBox1.SelectedIndex == 0)
            {
                habitacionSimple habitacionsimple = new habitacionSimple();
                habitacionsimple.Huesped = textBox2.Text;
                habitacionsimple.NumeroHabitacion = textBox1.Text;
                habitacionsimple.Cantidadnoches = noche;


            }
            if (comboBox1.SelectedIndex == 1)
            {
                habitacionDoble habitaciondoble = new habitacionDoble();
                habitaciondoble.NumeroHabitacion = textBox1.Text;
                habitaciondoble.Huesped = textBox2.Text;
                habitaciondoble.Cantidadnoches = noche;
                habitaciondoble.Tienebalcon = checkBox1.Checked;

                reservas.Add(habitaciondoble);
            }

            comboBox1.SelectedIndex = -1;
            textBox2.Clear();
            textBox1.Clear();
            textBox3.Clear();
        }

        private void button2_Click(object sender, EventArgs e) 
        {
            string habitacionessimples = "habitaciones simples: \n\n";
            string habitacionesdobles = "habitaciones dobles \n\n";
            int cantidadsimples = 0;
            int cantidaddobles = 0;

            if (comboBox1.SelectedIndex == 1)
            {
                foreach (var objeto in reservas)
                {
                    habitacionDoble habitacion = objeto as habitacionDoble;
                    habitacionesdobles += $" \n";
                    cantidaddobles += 1;
                }
            }
            label5.Text = $"{habitacionessimples}" +
                $"{habitacionesdobles} ";
            if (comboBox1.SelectedIndex == 0)
            {
                foreach (var objeto in reservas)
                {
                    habitacionSimple habitacion = objeto as habitacionSimple;
                    habitacionessimples += $" \n";
                    cantidadsimples += 1;
                }

               
            }
        }
    }
