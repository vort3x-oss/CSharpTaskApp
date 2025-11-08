# CSharpTaskApp
using System;
using System.Collections.Generic;
using System.IO;



namespace Experiment
{

    class Program
    {
        static string TaskFile = "tasks.txt";

        static void Main(string[] args)
        {

            Interface();

        }


        static void Interface()
        {
            bool running = true;
            while (running)
            {
                Console.WriteLine("1: Create a task\n2: View your tasks\n3: Exit");
                var key = Console.ReadKey(true).Key;
                switch (key)
                {
                    case ConsoleKey.D1:
                        CreateTask();
                        break;

                    case ConsoleKey.D2:
                        ViewTask();
                        break;

                    case ConsoleKey.D3:
                        running = ExitPage();
                        break;


                }
            }


        }


        //Complete
        static bool ExitPage()
        {
            Console.Clear();
            Console.WriteLine("Are you sure you want to exit?");


            while (true)
            {
                string choice = Console.ReadLine().ToLower();
                switch (choice) //case is what goes into choice
                {
                    case "yes":
                        Console.Clear();
                        Console.WriteLine("Have a nice day!");
                        Thread.Sleep(2000);
                        return false;
                        break;

                    case "no":
                        Console.Clear();
                        Console.WriteLine("Going back to the menu...");
                        Thread.Sleep(2000);
                        Console.Clear();
                        return true;
                        break;


                    default:
                        Console.Clear();
                        Console.WriteLine("Invalid choice, please type 'yes' or 'no'.");
                        break;

                }

            }

        }


        //Complete
        static void CreateTask()
        {
            if (!File.Exists(TaskFile))
            {
                Console.Clear();
                List<string> intro = new List<string> { "Welcome", "to", "our", "app" };
                foreach (string str in intro)
                {
                    Console.Write(str + " ");
                    Thread.Sleep(1000);
                }
                Console.WriteLine("\nCreate your first task by writing it below!");
                string firstTask = Console.ReadLine();
                File.WriteAllText(TaskFile, firstTask + Environment.NewLine);
                bool otherTasks = true;
                while (otherTasks)
                {
                    Console.Clear();
                    Console.WriteLine("Do you want to add other tasks?\nType 'yes' or 'no'.");
                    string finalAnswer = Console.ReadLine();
                    switch (finalAnswer)
                    {
                        case "yes":
                            Console.Clear();
                            Console.WriteLine("Enter your task.");
                            string anotherTask = Console.ReadLine().ToLower();
                            File.AppendAllText(TaskFile, anotherTask + Environment.NewLine);
                            Console.WriteLine("Task saved succesfully");
                            Thread.Sleep(1000);
                            Console.Clear();
                            Interface();
                            return;
                            break;

                        case "no":
                            Console.Clear();
                            Console.WriteLine("Alright.");
                            Thread.Sleep(1000);
                            Console.WriteLine("Going back to the menu...");
                            Thread.Sleep(1000);
                            Console.Clear();
                            Interface();
                            return;
                            otherTasks = false;
                            break;

                        default:
                            Console.Clear();
                            Console.WriteLine("Invalid choice, please type 'yes' or 'no'.");
                            break;
                    }
                }

            }




            else
            {
                Console.Clear();
                Console.WriteLine("Nice to see you here!");
                Thread.Sleep(500);
                Console.WriteLine("Add your task");
                string newTask = Console.ReadLine();
                File.AppendAllText(TaskFile, newTask + Environment.NewLine);
                bool newTasks = true;
                while (newTasks)
                {
                    Console.Clear();
                    Console.WriteLine("Do you want to add other tasks?\nType 'yes' or 'no'.");
                    string finalAnswer = Console.ReadLine();
                    switch (finalAnswer)
                    {
                        case "yes":
                            Console.Clear();
                            Console.WriteLine("Enter your task.");
                            string anotherTask = Console.ReadLine().ToLower();
                            File.AppendAllText(TaskFile, anotherTask + Environment.NewLine);
                            Console.WriteLine("Task saved succesfully");
                            Thread.Sleep(1000);
                            Console.Clear();
                            Interface();
                            return;
                            break;

                        case "no":
                            Console.Clear();
                            Console.WriteLine("Alright.");
                            Thread.Sleep(1000);
                            Console.WriteLine("Going back to the menu...");
                            Thread.Sleep(1000);
                            Console.Clear();
                            Interface();
                            return;
                            newTasks = false;
                            break;

                        default:
                            Console.Clear();
                            Console.WriteLine("Invalid choice, please type 'yes' or 'no'.");
                            break;
                    }
                }
            }

        }
        
        //Complete
        static void ViewTask()
        {
            if (!File.Exists(TaskFile))
            {
                Console.Clear();
                Console.WriteLine("You do not have any tasks for now!");
                Console.WriteLine("Press \'B\' to go back to the menu");
                while (true)
                {
                    var key = Console.ReadKey(true).Key;
                    if (key == ConsoleKey.B)
                    {
                        Console.Clear();
                        Console.WriteLine("Going back to the menu...");
                        Thread.Sleep(1000);
                        Console.Clear();
                        Interface();
                        return;
                    }
                    else
                    {
                        Console.Clear();
                        Console.WriteLine("Invalid choice. Press \'B\' to go back to main menu");

                    }
                }
            }

            else
            {
                Console.Clear();
                Console.WriteLine("Here are all your tasks");
                string[] allTasks = File.ReadAllLines(TaskFile);

                for (int i = 0; i < allTasks.Length; i++)
                {
                    Console.WriteLine($"{i + 1}: {allTasks[i]}");
                }
                Console.WriteLine("Press \'B\' to go back to the menu");
                while (true)
                {
                    var key = Console.ReadKey(true).Key;
                    if (key == ConsoleKey.B)
                    {
                        Console.Clear();
                        Console.WriteLine("Going back to the menu...");
                        Thread.Sleep(1000);
                        Console.Clear();
                        Interface();
                        return;
                    }
                    else
                    {
                        Console.Clear();
                        Console.WriteLine("Invalid choice. Press \'B\' to go back to main menu");

                    }
                }
            }
           
        }
        
    }
}
