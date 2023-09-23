using System;
using System.Drawing;
using System.Drawing.Printing;
using System.Windows.Forms;

namespace KG_P2
{
    public partial class Form1 : Form
    {
        static Graphics holst;
        static Pen pen_green;

        public Form1()
        {
            InitializeComponent();
        }

        private void Draw(object sender, EventArgs e)
        {
            pen_green = new Pen(Color.DarkBlue, 1);
            holst = CreateGraphics();
            holst.Clear(Color.White);

            int margin = 150;

            int centerX = this.ClientSize.Width / 2;
            int centerY = this.ClientSize.Height / 2;

            int triangleSize = Math.Min(this.ClientSize.Width, this.ClientSize.Height) / 2 - margin;


            var point1 = new PointF(centerX, centerY - triangleSize);
            var point2 = new PointF(centerX - (int)(triangleSize * Math.Sin(Math.PI / 3)), centerY + (int)(triangleSize * Math.Cos(Math.PI / 3)));
            var point3 = new PointF(centerX + (int)(triangleSize * Math.Sin(Math.PI / 3)), centerY + (int)(triangleSize * Math.Cos(Math.PI / 3)));

            holst.DrawLine(pen_green, point1, point2);
            holst.DrawLine(pen_green, point2, point3);
            holst.DrawLine(pen_green, point3, point1);

            FractalKoh(point1, point2, point3, 7);
            FractalKoh(point2, point3, point1, 7);
            FractalKoh(point3, point1, point2, 7);
        }

        static int FractalKoh(PointF p1, PointF p2, PointF p3, int iter)
        {
            if (iter > 0)
            {
                // средняя треть отрезка
                var p4 = new PointF((p2.X + 2 * p1.X) / 3, (p2.Y + 2 * p1.Y) / 3);
                var p5 = new PointF((2 * p2.X + p1.X) / 3, (p1.Y + 2 * p2.Y) / 3);

                // координаты вершины угла
                var ps = new PointF((p2.X + p1.X) / 2, (p2.Y + p1.Y) / 2);
                var pn = new PointF((4 * ps.X - p3.X) / 3, (4 * ps.Y - p3.Y) / 3);

                // рисуем его
                holst.DrawLine(pen_green, p4, pn);
                holst.DrawLine(pen_green, p5, pn);
                holst.DrawLine(pen_green, p4, p5);

                // рекурсивно вызываем функцию нужное число раз
                FractalKoh(p4, pn, p5, iter - 1);
                FractalKoh(pn, p5, p4, iter - 1);
                FractalKoh(p1, p4, new PointF((2 * p1.X + p3.X) / 3, (2 * p1.Y + p3.Y) / 3), iter - 1);
                FractalKoh(p5, p2, new PointF((2 * p2.X + p3.X) / 3, (2 * p2.Y + p3.Y) / 3), iter - 1);
            }
            return iter;
        }
    }
}
