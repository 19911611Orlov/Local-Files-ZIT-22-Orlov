import java.util.*;
 
import static java.util.Comparator.*;
 
class Contact {
    private String fName; // Имя
    private String lName; // Фамилия
    private List<String> numbers; // Лист с номерами
 
    // Конструктор класса Contact
    public Contact(String fName, String lName, List<String> numbers) {
        this.fName = fName;
        this.lName = lName;
        this.numbers = numbers;
    }
 
    // Возвращает полное имя
    public String getFullName() {
        return fName + " " + lName;
    }
 
    // Возвращает список номеров
    public List<String> getNumbers() {
        return numbers;
    }
 
    //Возваращает фамилию
    public String getLastName(String lname)
    {
        return lName;
    }
 
    //Возвращает имя
    public  String getFirstName(String fName)
    {
        return fName;
    }
    
    //Геттер для сортрировки по алфавиту
    public String getfname()
    {
        return fName;
    }
 
    // Устанавливает новое  имея
    public void setFirstName(String fName) {
        this.fName = fName;
    }
 
    // Устанавливает новую фамилию
    public void setLastName(String lName) {
        this.lName = lName;
    }
 
    // Устанавливает новый номер
    public void setPhoneNumbers(List<String> numbers) {
        this.numbers = numbers;
    }
}
 
class PhoneBook {
    private List<Contact> contacts; // Список контактов
 
    // Конструктор класса PhoneBook
    public PhoneBook() {
        contacts = new ArrayList<>();
    }
 
    // Добавляет новый контакт в телефонную книгу и сортирует её по полному имени контакта
    public void addContact(Contact contact) {
        contacts.add(contact);
        Collections.sort(contacts, comparing(Contact::getfname));
    }
 
    // Удаляет указанный контакт из телефонной книги
    public void removeContact(Contact contact) {
        contacts.remove(contact);
    }
 
    // Ищет контакты по заданной фамилии и возвращает список найденных контактов
    public List<Contact> searchByLastName(String lName) {
        List<Contact> results = new ArrayList<>();
        for (Contact contact : contacts) {
 
                results.add(contact);
 
        }
        return results;
    }
 
    // Ищет контакты по заданному номеру телефона и возвращает список найденных контактов
    public List<Contact> searchByPhoneNumber(String number) {
        List<Contact> results = new ArrayList<>();
        for (Contact contact : contacts) {
            if (contact.getNumbers().contains(number)) {
                results.add(contact);
            }
        }
        return results;
    }
 
    // Редактирует указанный контакт с заданными новыми данными
    public void editContact(Contact contact, String newFName, String newLName, List<String> newNumbers) {
        contact.setFirstName(newFName);
        contact.setLastName(newLName);
        contact.setPhoneNumbers(newNumbers);
    }
}
 
public class Main {
    public static void main(String[] args) {
        PhoneBook book = new PhoneBook(); // Создание новой телефонной книги
        Scanner scanner = new Scanner(System.in); // Создание объекта Scanner для считывания ввода пользователя
        int choice; // Переменная для хранения выбора пользователя
 
        do {
            // Вывод меню на экран
            System.out.println("Меню:");
            System.out.println("1. Поиск по номеру");
            System.out.println("2. Поиск по фамилии");
            System.out.println("3. Редактирование");
            System.out.println("4. Добавление");
            System.out.println("5. Удаление");
            System.out.println("0. Выход");
            System.out.print("Выберите пункт: ");
            choice = scanner.nextInt(); // Считывание выбора пользователя
            scanner.nextLine(); // Считывание символа новой строки после считывания числа
 
            // Обработка выбора пользователя
            switch (choice) {
                case 1:
                    // Поиск по номеру телефона
                    System.out.println("Введите номер телефона для поиска:");
                    String searchNumber = scanner.nextLine();
                    List<Contact> searchResultsByNumber = book.searchByPhoneNumber(searchNumber);
                    // Вывод результатов поиска
                    if (searchResultsByNumber.isEmpty()) {
                        System.out.println("Контакты не найдены.");
                    } else {
                        System.out.println("Найденные контакты:");
                        for (Contact contact : searchResultsByNumber) {
                            System.out.println(contact.getFullName() + ": " + contact.getNumbers());
                        }
                    }
                    break;
                case 2:
                    // Поиск по фамилии
                    System.out.println("Введите фамилию для поиска:");
                    String searchLName = scanner.nextLine();
                    List<Contact> searchResultsByLName = book.searchByLastName(searchLName);
                    // Вывод результатов поиска
                    if (searchResultsByLName.isEmpty()) {
                        System.out.println("Контакты не найдены.");
                    } else {
                        System.out.println("Найденные контакты:");
                        for (Contact contact : searchResultsByLName) {
                            System.out.println(contact.getFullName() + ": " + contact.getNumbers());
                        }
                    }
                    break;
                case 3:
                    // Редактирование контакта
                    System.out.println("Введите фамилию для редактирования:");
                    String editLName = scanner.nextLine();
                    List<Contact> editResults = book.searchByLastName(editLName);
                    // Редактирование найденного контакта
                    if (editResults.isEmpty()) {
                        System.out.println("Контакт не найден.");
                    } else {
                        for (Contact contact : editResults) {
                            System.out.println("Текущие данные контакта: " + contact.getFullName() + ": " + contact.getNumbers());
                            System.out.print("Введите новое имя: ");
                            String newFName = scanner.nextLine();
                            System.out.print("Введите новую фамилию: ");
                            String newLName = scanner.nextLine();
                            System.out.print("Введите новый номер телефона: ");
                            String newNumber = scanner.nextLine();
                            List<String> newNumbers = new ArrayList<>();
                            newNumbers.add(newNumber);
                            book.editContact(contact, newFName, newLName, newNumbers);
                            System.out.println("Контакт успешно отредактирован.");
                        }
                    }
                    break;
                case 4:
                    // Добавление нового контакта
                    System.out.print("Введите имя: ");
                    String addFName = scanner.nextLine();
                    System.out.print("Введите фамилию: ");
                    String addLName = scanner.nextLine();
                    System.out.print("Введите номер телефона: ");
                    String addNumber = scanner.nextLine();
                    List<String> addNumbers = new ArrayList<>();
                    addNumbers.add(addNumber);
                    Contact newContact = new Contact(addFName, addLName, addNumbers);
                    book.addContact(newContact);
                    System.out.println("Контакт успешно добавлен.");
                    break;
                case 5:
                    // Удаление контакта
                    System.out.println("Введите фамилию для удаления:");
                    String removeLName = scanner.nextLine();
                    List<Contact> removeResults = book.searchByLastName(removeLName);
                    // Удаление найденного контакта
                    if (removeResults.isEmpty()) {
                        System.out.println("Контакт не найден.");
                    } else {
                        for (Contact contact : removeResults) {
                            book.removeContact(contact);
                            System.out.println("Контакт успешно удален.");
                        }
                    }
                    break;
                case 0:
                    // Выход из программы
                    break;
                default:
                    // Обработка некорректного выбора пользователя
                    System.out.println("Некорректный выбор. Пожалуйста, выберите пункт от 0 до 5.");
            }
        } while (choice != 0); // Повторять цикл, пока пользователь не выберет 0
    }
}
 
