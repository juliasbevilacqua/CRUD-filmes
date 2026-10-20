using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
using MySql.Data;
using MySql.Data.MySqlClient;

namespace revisao_jj
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }
        string MysqlClientString = "Server = localhost; Port = 3306; User = root; " +
           "Database = bdcadastro; SSL Mode = 0";

        private void guna2Button2_Click(object sender, EventArgs e)
       
        {
           
        }

        private void guna2PictureBox5_Click(object sender, EventArgs e)
        {
           
        }

        private void guna2PictureBox6_Click(object sender, EventArgs e)
        {
            {
                try
                {
                    using (MySqlConnection conn = new MySqlConnection(MysqlClientString))
                    {
                        conn.Open();
                        string sql = "SELECT * FROM tbfilmes WHERE titulo LIKE @titulo";
                        using (MySqlDataAdapter da = new MySqlDataAdapter(sql, conn))
                        {
                            da.SelectCommand.Parameters.AddWithValue("@titulo", "%" + guna2TextBox2.Text + "%");
                            DataTable dt = new DataTable();
                            da.Fill(dt);
                            guna2DataGridView2.DataSource = dt;
                            if (guna2DataGridView2.Columns.Count >= 4)
                            {
                                guna2DataGridView2.Columns[0].Width = 40;
                                guna2DataGridView2.Columns[1].Width = 200;
                                guna2DataGridView2.Columns[2].Width = 200;
                                guna2DataGridView2.Columns[3].Width = 250;
                                guna2DataGridView2.Columns[4].Width = 250;
                            }

                            if (dt.Rows.Count == 0)
                            {
                                MessageBox.Show("Nenhum aluno encontrado.", "Filtro",
                                    MessageBoxButtons.OK, MessageBoxIcon.Information);
                            }
                        }
                    }
                }
                catch (Exception ex)
                {
                    MessageBox.Show("Erro ao realizar o filtro:\n" + ex.Message, "Erro",
                        MessageBoxButtons.OK, MessageBoxIcon.Error);
                }
            }
        }
    }
}




