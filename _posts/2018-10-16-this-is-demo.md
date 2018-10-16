---
layout: post
title: This is Demo
tags: [Test, Markdown]
---

Jekyll supports the use of [Markdown](http://daringfireball.net/projects/markdown/syntax) with inline HTML tags which makes it easier to quickly write posts with Jekyll, without having to worry too much about text formatting. A sample of the formatting follows.

Tables have also been extended from Markdown:

First Header  | Second Header
------------- | -------------
Content Cell  | Content Cell
Content Cell  | Content Cell

Here's an example of an image, which is included using Markdown:

![Image of a glass on a book]({{ site.baseurl }}/assets/img/pexels/book-glass.jpeg)

Highlighting for code in Jekyll is done using Base16 or Rouge. This theme makes use of Rouge by default.

{% highlight js %}
// count to ten
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;
using System.Data.OleDb;
using System.Management;
using System.Management.Instrumentation;
namespace RZ_Travels2018
{
    public partial class RZ_Travels2018Form : Form
    {

        cls_connectivity m = new cls_connectivity();
        int r, R1;
        public RZ_Travels2018Form()
        {
            InitializeComponent(); 
       
        }
        //For Control Enter Button Keys Forward
        protected override bool ProcessCmdKey(ref Message msg, Keys keyData)
        {
            switch (msg.WParam.ToInt32())
            {
                case 13:
                    if (this.ActiveControl is TextBox)
                    {
                        SendKeys.Send("{Tab}");
                        return true;
                    }
                    if (this.ActiveControl is ComboBox)
                    {
                        SendKeys.Send("{Tab}");
                        return true;
                    }
                    if (this.ActiveControl is DateTimePicker)
                    {
                        SendKeys.Send("{Tab}");
                        return true;
                    }

                    break;


            }
            return base.ProcessCmdKey(ref msg, keyData);
        }

        private void hide1()
        {
            string s = "select * from TBL_COMPANY";
            OleDbDataReader DR = m.selection(s);
            if (DR.Read() == true)
            {

            }
            else
            {

                //FRM_CREATECOMPANY cr = new FRM_CREATECOMPANY();
                //cr.Show();
                //this.Close();
            }

        }
        private void COMPANYDATA()
        {
            int A = 1;
            string selectq = "select F_COMPANYNAME,F_ADDRESS,F_MONO,F_TINNO FROM TBL_COMPANY where  F_CODE=" + A + "";
            OleDbDataReader DR = m.selection(selectq);
            DR.Read();
            //  lbl_title.Text = "       " + DR[0].ToString();
            lbl_name.Text =DR[0].ToString();
            //lbl_add.Text = DR[1].ToString();


        }
        public string GetMotherBoardID()
        {
            string s = "";
            ManagementObjectSearcher MOS = new ManagementObjectSearcher("Select * From Win32_BaseBoard");
            foreach (ManagementObject getserial in MOS.Get())
            {
                s = getserial["SerialNumber"].ToString();
            }
            return s;
        }

        private void getmotherbord()
        {
            COMPANYDATA();
            int FCODE = 1;
            string LIP = GetMotherBoardID();
            string S = "SELECT F_PICPATH FROM TBL_COMPANY";
            OleDbDataReader DR = m.selection(S);
            DR.Read();
            if (DR[0].ToString() == "")
            {
                string UP = "UPDATE TBL_COMPANY SET F_PICPATH='" + LIP + "' WHERE F_CODE=" + FCODE + "";
                m.insertion(UP);
            }
            else
            {
                if (LIP == DR[0].ToString())
                {
                 //   hide1();
                }
                else
                {
                    MessageBox.Show("YOU HAVE NOT PERMISSION TO USE THIS SOFTWARE " + "CONTACT ADMINISTRATIVE");
                    this.Close();
                    Frm_About ABOUT = new Frm_About();
                    ABOUT.Show();
                    Application.Exit();
                }
            }
        }
        private void MenuForm_Load(object sender, EventArgs e)
        {
            totalall();
            getmotherbord();
        }
        private void pnlview(Panel p)
        {
            pnlmaster.Visible = false;
         
            pnlbank.Visible = false;
            pnltransaction.Visible = false;
            pnlreport.Visible = false;
            pnltools.Visible = false;
            pnllogout.Visible = false;
            p.Visible = true;

        }
        private void btnview(Button b)
        {
            btnmaster.BackColor = Color.FromArgb(45, 45, 45);
          
            btnbank.BackColor = Color.FromArgb(45, 45, 45);
            btntransaction.BackColor = Color.FromArgb(45, 45, 45);
            btnreport.BackColor = Color.FromArgb(45, 45, 45);
            btntools.BackColor = Color.FromArgb(45, 45, 45);
            btnlogout.BackColor = Color.FromArgb(45, 45, 45);
            b.BackColor = Color.FromArgb(32, 32, 32);
        }
        private void btnmaster_Click(object sender, EventArgs e)
        {
              btnview(btnmaster);
              pnlview(pnlmaster);
              FRM_MasterFiles mm = new FRM_MasterFiles();
              mm.ShowDialog();
              btnview(btnextra);
              pnlview(pnlextra);
            
        }

       
        private void btnbank_Click(object sender, EventArgs e)
        {
              btnview(btnbank);
              pnlview(pnlbank);
              BankFiles bb = new BankFiles();
              bb.ShowDialog();
              btnview(btnextra);
              pnlview(pnlextra);
        }

        private void btntransaction_Click(object sender, EventArgs e)
        {
              btnview(btntransaction);
              pnlview(pnltransaction);
              FRM_TransactionFiles bb = new FRM_TransactionFiles();
              
              bb.ShowDialog();
              btnview(btnextra);
              pnlview(pnlextra);
        }

        private void btnreport_Click(object sender, EventArgs e)
        {
              btnview(btnreport);
              pnlview(pnlreport);
              Frm_Reportfiles bb = new Frm_Reportfiles();
              bb.ShowDialog();
              btnview(btnextra);
              pnlview(pnlextra);
        }

        private void btntools_Click(object sender, EventArgs e)
        {
              btnview(btntools);
              pnlview(pnltools);
              FRM_ToolFiles tt = new FRM_ToolFiles();
              tt.ShowDialog();
              btnview(btnextra);
              pnlview(pnlextra);
        }

        private void btnlogout_Click(object sender, EventArgs e)
        {
              btnview(btnlogout);
              pnlview(pnllogout);
              Frm_Login tt = new Frm_Login();
              tt.ShowDialog();
              btnview(btnextra);
              pnlview(pnlextra);
        }

        private void btnexit1_Click(object sender, EventArgs e)
        {
            Application.Exit();
        }

   
        private void btnminus_Click(object sender, EventArgs e)
        {
            this.WindowState = FormWindowState.Minimized;
        }
        private void hidepanel()
        {
            if (lblshowhide.Text == "Show Status")
            {
                pnlmain.Visible = true;
                lblshowhide.Top = 396;
                lblshowhide.Text = "Hide Status";
            }
            else
            {
                pnlmain.Visible = false;
                lblshowhide.Top = 90;
                lblshowhide.Text = "Show Status";
            }
        }
        private void lblshowhide_LinkClicked(object sender, LinkLabelLinkClickedEventArgs e)
        {
            hidepanel();
        }

        private void btnhide_Click(object sender, EventArgs e)
        {
            hidepanel();
        }

        private void getmethod(string str, TextBox l)
        {
          OleDbDataReader dr=m.selection(str);
          double dtot = 0;
            while (dr.Read())
          {
            dtot+=double .Parse (dr[0].ToString ());
          }
            l.Text = dtot.ToString();
        }
        private void totalall()
        {  
            long MONTH1 = long.Parse(dtpdate.Value.Month.ToString());

            string strexp = "select famount from tblexpense where fmonth=" + MONTH1 + "";
            string strdebit = "select famount from tbldebit where fmonth=" + MONTH1 + " and fmethod='DEBIT'";
            string strcredit = "select famount from tbldebit where fmonth=" + MONTH1 + " and fmethod='CREDIT'";
            string strcash = "select famount from tblgeneral where fmonth=" + MONTH1 + " and fmethod='CASH'";
            getmethod(strexp,lblexp);
            getmethod(strdebit,lbldebit);
            getmethod(strcredit,lblcredit);
            getmethod(strcash,lblcash);
            double dprofit = double.Parse(lblcredit.Text) + double.Parse(lblcash.Text);
            lblprofit.Text = dprofit.ToString();
        }

        private void btnsearch_Click(object sender, EventArgs e)
        {
            totalall();
        }

        private void timer_Tick(object sender, EventArgs e)
        {
            LBL_TIMER.Text = "Today is:  " + DateTime.Now.ToShortDateString() + " [ " + DateTime.Now.ToLongTimeString() + " ] ";

        }

        private void btnabout_Click(object sender, EventArgs e)
        {
            Frm_About aa = new Frm_About();
            aa.ShowDialog();
        }

        private void RZ_Travels2018Form_KeyUp(object sender, KeyEventArgs e)
        {
            if (e.KeyCode == Keys.F1)
            {
                Frm_ClearAcc cc = new Frm_ClearAcc();
                cc.ShowDialog();
            }
        }

        private void btnabout_Click_1(object sender, EventArgs e)
        {
            Frm_About ab = new Frm_About();
            ab.ShowDialog();
        }


       
    
    

       
       
       
       
 
    }
}

{% endhighlight %}

Type on Strap uses KaTeX to display maths. Equations such as $$S_n = a \times \frac{1-r^n}{1-r}$$ can be displayed inline.

Alternatively, they can be shown on a new line:

$$ f(x) = \int \frac{2x^2+4x+6}{x-2} $$
