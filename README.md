# python_project_hotel_management_system
I’m excited to share my first Python project—a Hospital Management System—built using core Python concepts without any advanced libraries. This project helped me strengthen my understanding of data structures, loops, functions, and user input handling while simulating a real-world hospital queue system.


specializations={i: [] for i in range(1,21)}

def add_dummy_data():
    specializations[3]=[
        {"name":"Dummy2","status":2},
        {"name":"Dummy5","status":2},
        {"name":"Dummy8","status":2},
        {"name":"Dummy1","status":1},
        {"name":"Dummy4","status":1},
        {"name":"Dummy7","status":1},
        {"name":"Dummy0","status":0},
        {"name":"Dummy3","status":0},
        {"name":"Dummy6","status":0},
        {"name":"Dummy9","status":0}
    ]

    specializations[6]=[
        {"name":"AnotherDummy0","status":0},
        {"name":"AnotherDummy1","status":0},
        {"name":"AnotherDummy2","status":0},
        {"name":"AnotherDummy3","status":0},
    ]

    specializations[9]=[
        {"name":"ThirdDummy0","status":1},
        {"name":"ThirdDummy1","status":1},
        {"name":"ThirdDummy2","status":1},
        {"name":"ThirdDummy3","status":1},
        {"name":"ThirdDummy4","status":1}
    ]
    
    # Specialization 13: 3 super urgent patients
    specializations[13]=[
        {"name":"ForthDummy0","status":2},
        {"name":"ForthDummy1","status":2},
        {"name":"ForthDummy2","status":2}
    ]
    
    # Specialization 14: 6 patients with mixed statuses
    specializations[14]=[
        {"name":"FifthDummy5","status":2},
        {"name":"FifthDummy6","status":2},
        {"name":"FifthDummy7","status":2},
        {"name":"FifthDummy8","status":1},
        {"name":"FifthDummy9","status":1},
        {"name":"FifthDummy10","status":1}
    ]

def add_patient():
    print("\n--- Add New Patient ---")

    while True:
        try:
            spec=int(input("Enter specialization (1-20): "))
            if 1<=spec<=20:
                break 
            else:
                print("Please enter a number between 1 and 20.")
        except:
            print("Please enter a valid number.")

    if len(specializations[spec])>=10:
        print("Sorry we can't add more patients for this specialization at the moment.")
        return
    
    name=input("Enter patient name: ").strip()
    if not name:
        print("Name cannot be empty.")
        return
    
    while True:
        try:
            status=int(input("Enter status (0 normal / 1 urgent / 2 super urgent):"))
            if status in [0,1,2]:
                break
            else:
                print("Please enter 0, 1, or 2.")
        except:
            print("Please enter a valid number (0, 1, or 2).")
    
    patient={"name":name,"status":status}

    if status==0:
        specializations[spec].append(patient)
    elif status==1:
        insert_pos=len(specializations[spec])
        for i,p in enumerate(specializations[spec]):
            if p["status"]==0:
                insert_pos=i
                break
        specializations[spec].insert(insert_pos,patient)
    else:
        insert_pos=len(specializations[spec])
        for i,p in enumerate(specializations[spec]):
            if p["status"]<2:
                insert_pos=i
                break
        specializations[spec].insert(insert_pos,patient)
    
    print(f"\npatient {name} added to specialization {spec}.")
    print(f"Specialization {spec} now has {len(specializations[spec])} patients.")

def print_patients():
    print("\n--- Current Patients in All Specializations ---")
    for spec in sorted(specializations.keys()):
        patients=specializations[spec]
        if not patients:
            continue

        print(f"\nSpecialization {spec}: There are {len(patients)} patients.")
        for patient in patients:
            status_str=""
            if patient["status"]==0:
                status_str="Normal"
            elif patient["status"]==1:
                status_str="Urgent"
            print(f"Patient: {patient['name']} is {status_str}")



def get_next_patient():
    print("\n--- Get Next Patient ---")

    while True:
        try:
            spec=int(input("Enter specialization (1-20): "))
            if 1<=spec<=20:
                break
            else:
                print("Please enter a number between 1 and 20.")
        except:
            print("Please enter a valid number.")

        if not specializations[spec]:
            print("No patients at the moment. Have rest, Dr")
            return
        
        next_patient=specializations[spec].pop(0)
        print(f"{next_patient['name']}, Please fo with the Dr")

def remove_leaving_patient():
    print("\n--- Remove Leaving Patient ---")

    while True:
        try:
            spec=int(input("Enter specialization (1-20): "))
            if 1<=spec<=20:
                break
            else:
                print("Please enter a number between 1 and 20.")
        except:
            print("Please enter a valid number.")

    name=input("Enter patient name: ").strip()

    found=False
    for i,patient in enumerate(specializations[spec]):
        if patient["name"]==name:
            found=True 
            print(f"Patient {name} removed from specialization {spec}.")
            break
    
    if not found:
        print(f"No patient with name '{name}' in specialization{spec}!")

def main():
    print("Welcome to Hospital Management System")
    add_dummy_data()  
    
    while True:
        print("\nProgram Options:")
        print("1) Add new patient")
        print("2) Print all patients")
        print("3) Get next patient")
        print("4) Remove a leaving patient")
        print("5) End the program")
        
        choice=input("Enter your choice (from 1 to 5): ")
        
        if choice=="1":
            add_patient()
        elif choice=="2":
            print_patients()
        elif choice=="3":
            get_next_patient()
        elif choice=="4":
            remove_leaving_patient()
        elif choice=="5":
            print("Thank you for using the Hospital Management System. Goodbye!")
            break
        else:
            print("Invalid choice. Please enter a number from 1 to 5.")

if __name__=="__main__":
    main()
