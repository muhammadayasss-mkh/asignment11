using System;
using System.Collections.Generic;
using System.Linq;

namespace BookSalesLINQ
{
    // Book class
    class Book
    {
        public int BookId { get; set; }
        public string Title { get; set; }
        public double Price { get; set; }
    }

    // Sales class
    class Sale
    {
        public int SaleId { get; set; }
        public int BookId { get; set; }
        public int Quantity { get; set; }
    }

    class Program
    {
        static void Main(string[] args)
        {
            // Book collection
            List<Book> books = new List<Book>()
            {
                new Book { BookId = 1, Title = "C# Basics", Price = 500 },
                new Book { BookId = 2, Title = "ASP.NET", Price = 700 },
                new Book { BookId = 3, Title = "LINQ Guide", Price = 600 }
            };

            // Sales collection
            List<Sale> sales = new List<Sale>()
            {
                new Sale { SaleId = 1, BookId = 1, Quantity = 2 },
                new Sale { SaleId = 2, BookId = 2, Quantity = 1 },
                new Sale { SaleId = 3, BookId = 3, Quantity = 3 }
            };

            // LINQ Join Query
            var result = from b in books
                         join s in sales on b.BookId equals s.BookId
                         select new
                         {
                             b.Title,
                             b.Price,
                             s.Quantity,
                             Total = b.Price * s.Quantity
                         };

            Console.WriteLine("Book Sales Details:\n");

            foreach (var item in result)
            {
                Console.WriteLine($"Title: {item.Title}");
                Console.WriteLine($"Price: {item.Price}");
                Console.WriteLine($"Quantity: {item.Quantity}");
                Console.WriteLine($"Total: {item.Total}");
                Console.WriteLine("----------------------");
            }

            // Total Sales Amount using LINQ
            double grandTotal = result.Sum(x => x.Total);
            Console.WriteLine("Grand Total Sales: " + grandTotal);

            Console.ReadLine();
        }
    }
}
