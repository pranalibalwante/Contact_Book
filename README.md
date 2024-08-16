class Contact:
    def __init__(self, name, phone, email, address):
        self.name = name
        self.phone = phone
        self.email = email
        self.address = address

    def __str__(self):
        return f"Name: {self.name}\nPhone: {self.phone}\nEmail: {self.email}\nAddress: {self.address}"

class ContactBook:
    def __init__(self):
        self.contacts = []

    def add_contact(self, contact):
        self.contacts.append(contact)
        print(f"\nContact '{contact.name}' added successfully.")

    def view_contacts(self):
        if not self.contacts:
            print("\nNo contacts available.")
        else:
            print("\nContact List:")
            for i, contact in enumerate(self.contacts, 1):
                print(f"{i}. {contact.name} - {contact.phone}")

    def search_contact(self, keyword):
        results = [contact for contact in self.contacts if keyword.lower() in contact.name.lower() or keyword in contact.phone]
        if not results:
            print("\nNo matching contacts found.")
        else:
            print("\nSearch Results:")
            for contact in results:
                print(contact)
                print("-" * 20)

    def update_contact(self, name):
        for contact in self.contacts:
            if contact.name.lower() == name.lower():
                print(f"\nUpdating contact: {contact.name}")
                contact.name = input("Enter new name (leave blank to keep current): ") or contact.name
                contact.phone = input("Enter new phone number (leave blank to keep current): ") or contact.phone
                contact.email = input("Enter new email (leave blank to keep current): ") or contact.email
                contact.address = input("Enter new address (leave blank to keep current): ") or contact.address
                print("\nContact updated successfully.")
                return
        print("\nContact not found.")

    def delete_contact(self, name):
        for contact in self.contacts:
            if contact.name.lower() == name.lower():
                self.contacts.remove(contact)
                print(f"\nContact '{name}' deleted successfully.")
                return
        print("\nContact not found.")

def main():
    contact_book = ContactBook()

    while True:
        print("\nContact Book Menu")
        print("1. Add Contact")
        print("2. View Contacts")
        print("3. Search Contact")
        print("4. Update Contact")
        print("5. Delete Contact")
        print("6. Exit")

        choice = input("Choose an option: ")

        if choice == "1":
            name = input("Enter name: ")
            phone = input("Enter phone number: ")
            email = input("Enter email: ")
            address = input("Enter address: ")
            contact = Contact(name, phone, email, address)
            contact_book.add_contact(contact)
        elif choice == "2":
            contact_book.view_contacts()
        elif choice == "3":
            keyword = input("Enter name or phone number to search: ")
            contact_book.search_contact(keyword)
        elif choice == "4":
            name = input("Enter the name of the contact to update: ")
            contact_book.update_contact(name)
        elif choice == "5":
            name = input("Enter the name of the contact to delete: ")
            contact_book.delete_contact(name)
        elif choice == "6":
            break
        else:
            print("Invalid choice. Please try again.")

if __name__ == "__main__":
    main()
