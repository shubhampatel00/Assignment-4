# Assignment-4
using System;
using System.Collections.Generic;

namespace COMP10066_Lab4
{
    /**
     * Library of statistical functions using Generics for different statistical
     * calculations.
     * 
     * see http://www.calculator.net/standard-deviation-calculator.html
     * for sample standard deviation calculations
     *
     * @author Joey Programmer
     */

    public class A4
    {
        /// <summary>
        /// Calculates and returns the average of the list of doublesa
        /// </summary>
        /// <param name="x"></param>
        /// <param name="incneg"></param>
        /// <returns>additon of all the numbers / total numbers</returns>
        public static double Average(List<double> x, bool incneg)
        {
            double s = Sum(x, incneg);
            int c = 0;
            for (int i = 0; i < x.Count; i++)
            {
                if (incneg || x[i] >= 0)
                {
                    c++;
                }
            }
            if (c == 0)
            {
                throw new ArgumentException("no values are > 0");
            }
            return s / c;
        }
        /// <summary>
        /// Calculates and returns the sum of the list of doubles
        /// </summary>
        /// <param name="x"></param>
        /// <param name="incneg"></param>
        /// <returns>Addition of all the numbers in the list</returns>
        public static double Sum(List<double> x, bool incneg)
        {
            if (x.Count < 0)
            {
                throw new ArgumentException("x cannot be empty");
            }

            double sum = 0.0;
            foreach (double val in x)
            {
                if (incneg || val >= 0)
                {
                    sum += val;
                }
            }
            return sum;
        }
        /// <summary>
        /// Calculates and returns the median
        /// </summary>
        /// <param name="data"></param>
        /// <returns>(data[data.Count / 2] + data[data.Count / 2 - 1]) / 2</returns>
        public static double Median(List<double> data)
        {
            if (data.Count == 0)
            {
                throw new ArgumentException("Size of array must be greater than 0");
            }

            data.Sort();

            double median = data[data.Count / 2];
            if (data.Count % 2 == 0)
                median = (data[data.Count / 2] + data[data.Count / 2 - 1]) / 2;

            return median;
        }
        /// <summary>
        /// calculates Standard Deviation
        /// </summary>
        /// <param name="data"></param>
        /// <returns>Squareroot(s / (total count of data - 1))</returns>
        public static double standardDev(List<double> data)
        {
            if (data.Count <= 1)
            {
                throw new ArgumentException("Size of array must be greater than 1");
            }

            int n = data.Count;
            double s = 0;
            double a = Average(data, true);

            for (int i = 0; i < n; i++)
            {
                double v = data[i];
                s += Math.Pow(v - a, 2);
            }
            double stdev = Math.Sqrt(s / (n - 1));
            return stdev;
        }

        /// <summary>
        ///  Simple set of tests that confirm that functions operate correctly
        /// </summary>
        /// <param name="args"></param>
        static void Main(string[] args)
        {
            List<Double> testDataD = new List<Double> { 2.2, 3.3, 66.2, 17.5, 30.2, 31.1 };

            Console.WriteLine("The sum of the array = {0}", Sum(testDataD, true));

            Console.WriteLine("The average of the array = {0}", Average(testDataD, true));

            Console.WriteLine("The median value of the Double data set = {0}", Median(testDataD));

            Console.WriteLine("The sample standard deviation of the Double test set = {0}\n", standardDev(testDataD));
        }
    }
}
