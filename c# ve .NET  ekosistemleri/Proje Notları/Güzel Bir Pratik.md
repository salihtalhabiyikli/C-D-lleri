```cs
using System;

  

namespace kalitim

{  

    public class Cokgen

    {

        protected void Main(int W ,int l)

        {

            Console.WriteLine("alan:" + (W * l));

            Console.WriteLine("çevre:" + (2 * (W + l)));    

        }

}

public class Dikdortgen : Cokgen

 {

        public int genislik,yukseklik;

        public void AlanHesapla()

        {

            int cevre=2*(genislik+yukseklik);

            Console.WriteLine("çevre:" + cevre);

            Main(genislik,yukseklik );

        }

  

        public void CevreHesapla()

        {

            int cevre = 2 * (genislik + yukseklik);

            Console.WriteLine("çevre:" + cevre);

        }

    }  

  

    public class Kare :Cokgen

    {

        public int kenar;

        public void AlanHesapla()

        {

            int cevre = 4 * kenar;

            Console.WriteLine("çevre:" + cevre);

            Main(kenar, kenar);

        }

        public void CevreHesapla()

        {

            int cevre = 4 * kenar;

            Console.WriteLine("çevre:" + cevre);

        }  

    }

}
```