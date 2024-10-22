using System;
using System.Timers;

namespace AlarmSystem
{
    class Program
    {
        static Timer alarmTimer;
        static bool isAlarmActive = false;

        static void Main(string[] args)
        {
            Console.WriteLine("Добро пожаловать в систему сигнализации!");

            while (true)
            {
                Console.WriteLine("\nВыберите действие:");
                Console.WriteLine("1. Включить сигнализацию");
                Console.WriteLine("2. Выключить сигнализацию");
                Console.WriteLine("3. Выйти");

                string choice = Console.ReadLine();

                switch (choice)
                {
                    case "1":
                        StartAlarm();
                        break;
                    case "2":
                        StopAlarm();
                        break;
                    case "3":
                        Environment.Exit(0);
                        break;
                    default:
                        Console.WriteLine("Неверный выбор. Попробуйте снова.");
                        break;
                }
            }
        }

        static void StartAlarm()
        {
            if (!isAlarmActive)
            {
                Console.WriteLine("Сигнализация включена!");
                isAlarmActive = true;

                // Установка таймера для срабатывания сигнализации (например, через 5 секунд)
                alarmTimer = new Timer(5000);
                alarmTimer.Elapsed += AlarmTimer_Elapsed;
                alarmTimer.Start();
            }
            else
            {
                Console.WriteLine("Сигнализация уже включена.");
            }
        }

        static void StopAlarm()
        {
            if (isAlarmActive)
            {
                Console.WriteLine("Сигнализация выключена!");
                isAlarmActive = false;
                alarmTimer.Stop();
            }
            else
            {
                Console.WriteLine("Сигнализация не включена.");
            }
        }

        static void AlarmTimer_Elapsed(object sender, ElapsedEventArgs e)
        {
            Console.WriteLine("!!! СИГНАЛ ТРЕВОГИ !!!");
            // Здесь можно добавить звуковой сигнал или другие действия при срабатывании сигнализации.
            // Например, можно отправить уведомление на мобильный телефон.
        }
    }
}
