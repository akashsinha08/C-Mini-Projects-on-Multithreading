# C++ -Mini-Projects-on-Multithreading
Mini Projects C++ using multi-threading and mutual exclusion principles
1. Vowel Count
This program counts all vowels in a given text files using multithreading. Mutual exclusion is used to lock processing to avoid conflicts.
2. Word Count
This program count the occurence of a particular word or all words in a big file using multithreading and filestream.
3. Sleeping Barber Problem
The famous wikipedia interprocessing problem that uses mutual exlusion and semaphores to synchronize a barber and his or her customers such that each customer has his or her hair cut in order.However this project changes the problem to multiple sleeping barbers problem where many customers visit a barbershop and receive a haircut service from any one available among barbers in the shop.

General Idea:

A barbershop consists of a waiting room with n chairs and a barber room with m barber chairs. If there are no customers to be served, all the barbers go to sleep. If a customer enters the barbershop and all chairs are occupied, then the customer leaves the shop. If all the barbers are busy but chairs are available, then the customer sits in one of the free chairs. If the barbers are asleep, the customer wakes up one of the barbers.
