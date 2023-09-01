using System;

// Define the Imylterator interface
public interface Imylterator
{
    int Next();
    void Begin();
    bool HasNext();
}

// Define the myCollection class
public class myCollection
{
    private int[] arr = new int[10000];
    private int tos = -1;
    private int nav = -1;

    public void Add(int i)
    {
        if (tos < 9999)
        {
            tos++;
            arr[tos] = i;
        }
    }

    public Imylterator GetIterator()
    {
        return new myIterator(this);
    }
}

// Define the myIterator class that implements Imylterator
public class myIterator : Imylterator
{
    private myCollection collection;

    public myIterator(myCollection c)
    {
        collection = c;
    }

    public int Next()
    {
        if (collection.tos != -1 && nav <= collection.tos)
        {
            int value = collection.arr[nav];
            nav++;
            return value;
        }
        throw new InvalidOperationException("No more elements.");
    }

    public void Begin()
    {
        if (collection.tos > -1)
        {
            nav = 0;
        }
    }

    public bool HasNext()
    {
        return nav <= collection.tos;
    }
}

class Program
{
    static void Main(string[] args)
    {
        myCollection c1 = new myCollection();

        for (int i = 1; i <= 10; i++)
        {
            c1.Add(i);
        }

        Imylterator it = c1.GetIterator();
        it.Begin();

        while (it.HasNext())
        {
            int nextValue = it.Next();
            Console.WriteLine($"Next value: {nextValue}");
        }
    }
}
