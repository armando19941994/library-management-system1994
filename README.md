# Lista per memorizzare i libri come dizionari
library_books = []

def add_book():
    """Aggiunge un nuovo libro alla biblioteca."""
    title = input("Enter the book title: ")
    author = input("Enter the author: ")
    isbn = input("Enter the ISBN: ")

    # Controlla se l'ISBN esiste già
    for book in library_books:
        if book['isbn'] == isbn:
            print("Error: ISBN already exists.")
            return

    # Aggiunge il libro come dizionario alla lista
    new_book = {
        'title': title,
        'author': author,
        'isbn': isbn,
        'checked_out': False
    }
    library_books.append(new_book)
    print("Book added successfully!")

def search_book():
    """Cerca un libro per titolo nella biblioteca."""
    title = input("Enter the title of the book you are searching for: ")
    found_books = [book for book in library_books if book['title'].lower() == title.lower()]

    if found_books:
        print("Books found:")
        for book in found_books:
            status = "Checked out" if book['checked_out'] else "Available"
            print(f"Title: {book['title']}, Author: {book['author']}, ISBN: {book['isbn']}, Status: {status}")
    else:
        print("No book found with that title.")

def view_inventory():
    """Mostra l'inventario completo dei libri."""
    if library_books:
        print("Library Inventory:")
        for book in library_books:
            status = "Checked out" if book['checked_out'] else "Available"
            print(f"Title: {book['title']}, Author: {book['author']}, ISBN: {book['isbn']}, Status: {status}")
    else:
        print("No books in the inventory.")

def check_out_book():
    """Permette di prendere in prestito un libro."""
    isbn = input("Enter the ISBN of the book to check out: ")
    for book in library_books:
        if book['isbn'] == isbn:
            if book['checked_out']:
                print("The book is already checked out.")
            else:
                book['checked_out'] = True
                print("Book checked out successfully!")
            return
    print("ISBN not found in the library.")

def check_in_book():
    """Permette di restituire un libro."""
    isbn = input("Enter the ISBN of the book to check in: ")
    for book in library_books:
        if book['isbn'] == isbn:
            if not book['checked_out']:
                print("The book is already available.")
            else:
                book['checked_out'] = False
                print("Book checked in successfully!")
            return
    print("ISBN not found in the library.")

def main_menu():
    """Menu principale del sistema di gestione della biblioteca."""
    while True:
        print("\n--- Library Management System ---")
        print("1. Add Book")
        print("2. Search Book by Title")
        print("3. View Inventory")
        print("4. Check Out Book")
        print("5. Check In Book")
        print("6. Exit")
        
        choice = input("Choose an option: ")

        if choice == '1':
            add_book()
        elif choice == '2':
            search_book()
        elif choice == '3':
            view_inventory()
        elif choice == '4':
            check_out_book()
        elif choice == '5':
            check_in_book()
        elif choice == '6':
            print("Exiting the system. Goodbye!")
            break
        else:
            print("Invalid choice. Please try again.")

# Avvio del sistema di gestione della biblioteca
if __name__ == "__main__":
    main_menu()
