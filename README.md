# vorislik-

static void Main(string[] args)
{
    Console.WriteLine("Enter the size of the matrix: ");
    int size = int.Parse(Console.ReadLine());
    DTR_MATRIX matrix = new DTR_MATRIX(size);
    Console.WriteLine("Enter the elements of the matrix: ");
    matrix.ReadValues();
    double det = matrix.CalculateDeterminant();
    Console.WriteLine("Determinant of the matrix is: " + det);
    Console.ReadLine();
}


class MATRIX
{
    int n;
    double[,] elements;

    public MATRIX(int size)
    {
        n = size;
        elements = new double[n, n];
    }

    public void ReadValues()
    {
        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < n; j++)
            {
                elements[i, j] = double.Parse(Console.ReadLine());
            }
        }
    }

    public void PrintValues()
    {
        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < n; j++)
            {
                Console.Write(elements[i, j] + " ");
            }
            Console.WriteLine();
        }
    }
}

class DTR_MATRIX : MATRIX
{
    public DTR_MATRIX(int size) : base(size) { }

    public double CalculateDeterminant()
    {
        double det = 0;
        if (n == 1)
            return elements[0, 0];
        else if (n == 2)
            return (elements[0, 0] * elements[1, 1]) - (elements[0, 1] * elements[1, 0]);
        else
        {
            for (int k = 0; k < n; k++)
            {
                MATRIX minor = new MATRIX(n - 1);
                int minor_i = 0;
                for (int i = 1; i < n; i++)
                {
                    int minor_j = 0;
                    for (int j = 0; j < n; j++)
                    {
                        if (j == k)
                            continue;
                        minor.elements[minor_i, minor_j] = elements[i, j];
                        minor_j++;
                    }
                    minor_i++;
                }
                det += Math.Pow(-1, k) * elements[0, k] * (new DTR_MATRIX(n - 1)).CalculateDeterminant();
            }
            return det;
        }
    }
}
