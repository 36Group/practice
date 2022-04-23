# practice
first practice
// faezeh alizadeh
// faezeh roshan kalati

#include <iostream>
#include <conio.h>
#include <cstring>
#include <fstream>

using namespace std;

enum Os
{
    iOS = 0,
    Android = 1,
    windows_phone = 2
};
enum Ram
{
    r2GB = 2,
    r4GB = 4,
    r6GB = 6,
    r8GB = 8,
    r12GB = 12,
    r16GB = 16,
    r32GB = 32,
    r64GB = 64
};
enum Storage
{
    s16GB = 16,
    s32GB = 32,
    s64GB = 64,
    s128GB = 128,
    s256GB = 256,
    s512GB = 512,
    s1TB = 1000,
    s2TB = 2000
};
enum Color
{
    white = 0,
    black = 1,
    Else = 2
};

struct Mobiles
{
    char name[20];
    char company[20];
    Os os;
    Ram ram;
    Storage storage;
    unsigned long int price;
    Color color;
    int count;
    int sell_number;
};

Mobiles *add_phone(Mobiles *, int &, Mobiles);
Mobiles add_phone(Mobiles, int);
Mobiles *remove_phone(int &, int);
void swap(Mobiles &, Mobiles &);
void sort_by_price(Mobiles *, int);
int search(Mobiles *, int, char[], char[]);
Mobiles change_mobile_info(Mobiles);
Mobiles sell_a_phone(Mobiles *, int);
void print_phones(Mobiles *, int);
void most_sold_item(Mobiles *, int);

void save_into_a_file(Mobiles *, int);
long size_of_file();
Mobiles *load_from_a_file(long);

int main()
{
    Mobiles *new_m = new Mobiles[0];
    int new_size = 0;
    int n1 = 0;
    long file_len;

    ifstream f4("mobile.file", ios::binary);

    if (f4)
    {
        file_len = size_of_file();
        new_m = load_from_a_file(file_len);
    }

    while (n1 != 9)
    {
        cout << "Choose a number: \n \n1- Add a phone  \n2- Remove a phone  \n3- Sort phones by price  \n4- Search a phone  \n5- Change mobile info  \n6- Sell a phone  \n7- Print phones  \n8- Print phones sorted by the most sold to the least  \n9- Quit  \n\n";
        cin >> n1;

        switch (n1)
        {
        case 1: // ezafe kardane mobile ha
        {
            string n2;
            Mobiles mobile;
            bool exists = false;

            do
            {
                cout << "Enter name of the mobile: \n";
                cin >> mobile.name;

                cout << "Enter name of the company: \n";
                cin >> mobile.company;

                int index2;
                index2 = search(new_m, new_size, mobile.name, mobile.company);

                if (index2 != -1)
                {
                    int n2;
                    cout << "How many of these phones are there? \n";
                    cin >> n2;
                    exists = true;

                    // ezafe kardan mojoodi mobile
                    new_m[index2] = add_phone(new_m[index2], n2);
                }

                else if (index2 == -1)
                {
                    // gereftan baghi ettelaat
                    int enum1, enum2, enum3, enum4;
                    cout << "Enter price: \n";
                    cin >> mobile.price;
                    cout << "Enter the count of this phone : \n";
                    cin >> mobile.count;
                    cout << "How many of these phones are sold? \n";
                    cin >> mobile.sell_number;
                    cout << "Enter a number : (iOS = 0 ,Android = 1 ,windows_phone = 2) \n";
                    cin >> enum1;

                    if (enum1 == 0)
                    {
                        mobile.os = iOS;
                    }
                    else if (enum1 == 1)
                    {
                        mobile.os = Android;
                    }
                    else if (enum1 == 2)
                    {
                        mobile.os = windows_phone;
                    }

                    cout << "Enter the amount of RAM :2,4,6, 8,12,16,32,64 (GB)\n";
                    cin >> enum2;
                    switch (enum2)
                    {
                    case 2:
                        mobile.ram = r2GB;
                        break;
                    case 4:
                        mobile.ram = r4GB;
                        break;
                    case 6:
                        mobile.ram = r6GB;
                        break;
                    case 8:
                        mobile.ram = r8GB;
                        break;
                    case 12:
                        mobile.ram = r12GB;
                        break;
                    case 16:
                        mobile.ram = r16GB;
                        break;
                    case 32:
                        mobile.ram = r32GB;
                        break;
                    case 64:
                        mobile.ram = r64GB;
                        break;

                    default:
                        break;
                    }

                    cout << "Enter the amount of storage : 16,32,64,128,256,512,1000,2000 (GB)\n";
                    cin >> enum3;
                    switch (enum3)
                    {
                    case 16:
                        mobile.storage = s16GB;
                        break;
                    case 32:
                        mobile.storage = s32GB;
                        break;
                    case 64:
                        mobile.storage = s64GB;
                        break;
                    case 128:
                        mobile.storage = s128GB;
                        break;
                    case 256:
                        mobile.storage = s256GB;
                        break;
                    case 512:
                        mobile.storage = s512GB;
                        break;
                    case 1000:
                        mobile.storage = s1TB;
                        break;
                    case 2000:
                        mobile.storage = s2TB;
                        break;

                    default:
                        break;
                    }

                    cout << "Enter color : (White = 0 , black = 1 , else = 2) \n";
                    cin >> enum4;
                    if (enum4 == 0)
                    {
                        mobile.color = white;
                    }
                    else if (enum4 == 1)
                    {
                        mobile.color = black;
                    }
                    else if (enum4 == 2)
                    {
                        mobile.color = Else;
                    }

                    // vared kardan be array
                    new_m = add_phone(new_m, new_size, mobile);
                    cout << "_________________\n This mobile is saved in the list .\n\n\n";
                }

                cout << "Do you want to continue? Y/N \n";
                cin >> n2;
            } while (n2 == "y" || n2 == "Y");

            break;
        }

        case 2: // hazfe yek mobile az array
        {
            Mobiles m2;

            cout << "Enter name of the mobile you want to delete : \n";
            cin >> m2.name;

            cout << "Enter company of the mobile you want to delete : \n";
            cin >> m2.company;

            int index3;
            index3 = search(new_m, new_size, m2.name, m2.company);

            if (index3 != -1)
            {
                // hazfe in mobile
                new_m = remove_phone(new_size, index3);
                cout << "The mobile is deleted. \n";
            }

            else if (index3 == -1)
            {
                cout << "There isn't this phone in the store. \n";
            }

            break;
        }

        case 3: // daste bandi list bar asase gheimat
        {
            sort_by_price(new_m, new_size);
            cout << "The list is sorted by price . \n";

            break;
        }

        case 4: // search mobile va chap
        {
            int index;
            char search_name[20], search_company[20];

            cout << "Enter the name of the mobile you want to search : \n ";
            cin >> search_name;

            cout << "Enter the company of the mobile you want to search : \n ";
            cin >> search_company;

            index = search(new_m, new_size, search_name, search_company);

            if (index == -1)
            {
                cout << "There isn't this phone in the store. \n";
            }
            else
            {
                cout << "__________________\n";
                cout << "name of the mobile : \n"
                     << new_m[index].name;
                cout << "\ncompany of the mobile : \n"
                     << new_m[index].company;
                cout << "\nprice of the mobile : \n"
                     << new_m[index].price;
                cout << "\ncount of the mobile : \n"
                     << new_m[index].count;
                cout << "\nsellnumber of the mobile : \n"
                     << new_m[index].sell_number;
                cout << "\nOs: \n"
                     << new_m[index].os;
                cout << "\nRAM: \n"
                     << new_m[index].ram;
                cout << "\nstorage: \n"
                     << new_m[index].storage;
                cout << "\ncolor: \n"
                     << new_m[index].color << endl;
            }

            break;
        }

        case 5: // avaz kardane ghesmat haye delkhah az yek mobile
        {
            Mobiles change;
            cout << "Enter name of the mobile you want to change it's information : \n";
            cin >> change.name;

            cout << "Enter company of the mobile you want to change it's information : \n";
            cin >> change.company;

            int index4;
            index4 = search(new_m, new_size, change.name, change.company);

            if (index4 != -1)
            {
                // avaz kardane etelaat
                new_m[index4] = change_mobile_info(change);
            }
            else if (index4 == 0)
            {
                cout << "There isn't this phone in the store. \n";
            }

            break;
        }

        case 6: // forosh yek mobile va avaz kardane etelaate an
        {
            Mobiles sold_mobile;
            cout << "Enter name of the mobile which is sold : \n";
            cin >> sold_mobile.name;

            cout << "Enter company of the mobile which is sold : \n";
            cin >> sold_mobile.company;

            int index5;
            index5 = search(new_m, new_size, sold_mobile.name, sold_mobile.company);

            if (index5 != -1)
            {
                // foroosh

                new_m[index5] = sell_a_phone(new_m, index5);
                cout << "ok\n";
            }

            else if (index5 == -1)
            {
                cout << "There isn't this phone in the store. \n";
            }

            break;
        }

        case 7: // print hame array
        {
            print_phones(new_m, new_size);
            break;
        }

        case 8: // print bar asas bishtarin forosh
        {
            most_sold_item(new_m, new_size);
            break;
        }
        case 9: // save dar file va khorooj
        {
            save_into_a_file(new_m, new_size);
            break;
        }
        }
    }
    delete[] new_m;
    getch();
    return 0;
}

// choice 1

Mobiles *add_phone(Mobiles *new_mobile, int &size, Mobiles mo)
{
    size++;

    Mobiles *real_mobile;
    real_mobile = new Mobiles[size];

    for (int i = 0; i < size; i++)
    {
        real_mobile[i] = new_mobile[i];
    }

    real_mobile[size - 1] = mo;

    delete[] new_mobile;

    return real_mobile;
}

Mobiles add_phone(Mobiles m, int a2)
{
    m.count += a2;
    return m;
}

// choice 2

Mobiles *remove_phone(int &size, int a3)
{
    Mobiles *deleted_mobile = new Mobiles[size];

    for (int i = a3; i < size; i++)
    {
        // deleted_mobile[i] = deleted_mobile[i + 1];
        swap(deleted_mobile[i], deleted_mobile[i + 1]);
    }

    size--;

    return deleted_mobile;
}

// choice 3

void swap(Mobiles &a, Mobiles &b)
{
    Mobiles temp;
    temp = a;
    a = b;
    b = temp;
}

void sort_by_price(Mobiles *array, int size)
{
    Mobiles *end, *min, *i;
    end = array + size - 1;

    for (; array < end; array++)
    {
        min = array; // search minimum
        for (i = array + 1; i <= end; i++)
        {
            if (i->price < min->price)
            {
                min = i;
            }
        }
        swap(*array, *min);
    }
}

// choice 4

int search(Mobiles *all_mobiles, int size, char sname[20], char scompany[20])
{
    for (int i = 0; i < size; i++)
    {
        if ((strcmp(all_mobiles[i].name, sname) == 0) && (strcmp(all_mobiles[i].company, scompany) == 0)) // strcmp
        {
            return i;
        }
    }
    return -1;
}

// choice 5

Mobiles change_mobile_info(Mobiles cmobile)
{
    int x, x1, x2, x3, x4;
    char x5;
    do
    {
        cout << "_______________________\n";
        cout << "What item do you want to change?Enter a number: \n1.name .2. company .3. Os .4. Ram .5. storage .6. price .7. color .8. count .9. sell_number \n";
        cin >> x;

        switch (x)
        {
        case 1:
        {
            cout << "Enter a new name :\n ";
            cin >> cmobile.name;
            break;
        }
        case 2:
        {
            cout << "Enter a new os :\n ";
            cin >> cmobile.company;
            break;
        }
        case 3:
        {
            cout << "Enter a number for new os : (iOS = 0 ,Android = 1 ,windows_phone = 2) \n";
            cin >> x1;
            if (x1 == 0)
            {
                cmobile.os = iOS;
            }
            else if (x1 == 1)
            {
                cmobile.os = Android;
            }
            else if (x1 == 2)
            {
                cmobile.os = windows_phone;
            }
            break;
        }
        case 4:
        {
            cout << "Enter the amount of new RAM :2,4,6, 8,12,16,32,64 (GB)\n";
            cin >> x2;
            switch (x2)
            {
            case 2:
                cmobile.ram = r2GB;
                break;
            case 4:
                cmobile.ram = r4GB;
                break;
            case 6:
                cmobile.ram = r6GB;
                break;
            case 8:
                cmobile.ram = r8GB;
                break;
            case 12:
                cmobile.ram = r12GB;
                break;
            case 16:
                cmobile.ram = r16GB;
                break;
            case 32:
                cmobile.ram = r32GB;
                break;
            case 64:
                cmobile.ram = r64GB;
                break;

            default:
                break;
            }
            break;
        }

        case 5:
        {
            cout << "Enter the amount of new storage : 16,32,64,128,256,512,1000,2000 (GB)\n";
            cin >> x3;
            switch (x3)
            {
            case 16:
                cmobile.storage = s16GB;
                break;
            case 32:
                cmobile.storage = s32GB;
                break;
            case 64:
                cmobile.storage = s64GB;
                break;
            case 128:
                cmobile.storage = s128GB;
                break;
            case 256:
                cmobile.storage = s256GB;
                break;
            case 512:
                cmobile.storage = s512GB;
                break;
            case 1000:
                cmobile.storage = s1TB;
                break;
            case 2000:
                cmobile.storage = s2TB;
                break;

            default:
                break;
            }

            break;
        }

        case 6:
        {
            cout << "Enter price: \n";
            cin >> cmobile.price;
            break;
        }
        case 7:
        {
            cout << "Enter new color : (White = 0 , black = 1 , else = 2";
            cin >> x4;
            if (x4 == 0)
            {
                cmobile.color = white;
            }
            else if (x4 == 1)
            {
                cmobile.color = black;
            }
            else if (x4 == 2)
            {
                cmobile.color = Else;
            }
            break;
        }
        case 8:
        {
            cout << "Enter the new count of this phone : \n";
            cin >> cmobile.count;
            break;
        }
        case 9:
        {
            cout << "How many of these phones are sold now? \n";
            cin >> cmobile.sell_number;
            break;
        }

        default:
            break;
        }

        cout << "Do you want to change anything else? ( y/n )\n";
        cin >> x5;
    } while (x5 == 'y' || x5 == 'Y');

    return cmobile;
}

// choice 6

Mobiles sell_a_phone(Mobiles *sellmobile, int z)
{
    sellmobile[z].count--;
    sellmobile[z].sell_number++;

    return sellmobile[z];
}

// choice 7
void print_phones(Mobiles *allmobiles, int size)
{

    cout << "***********\n    The list of the mobiles:\n\n\n";
    if (size == 0)
    {
        cout << "The list is empty. \n";
    }
    else
    {
        for (int i = 0; i < size; i++)
        {
            cout << "the " << i + 1 << "th mobile:\n\n";
            cout << "name: " << allmobiles[i].name << endl;
            cout << "company: " << allmobiles[i].company << endl;

            switch (allmobiles[i].os)
            {
            case iOS:
                cout << "Os: iOS" << endl;
                break;
            case Android:
                cout << "Os: Android" << endl;
                break;
            case windows_phone:
                cout << "Os: windows_phone" << endl;
                break;
            }

            switch (allmobiles[i].ram)
            {
            case r2GB:
                cout << "RAM: 2GB " << endl;
                break;

            case r4GB:
                cout << "RAM: 4GB " << endl;
                break;

            case r6GB:
                cout << "RAM: 6GB " << endl;
                break;

            case r8GB:
                cout << "RAM: 8GB " << endl;
                break;

            case r12GB:
                cout << "RAM: 12GB " << endl;
                break;

            case r16GB:
                cout << "RAM: 16GB " << endl;
                break;

            case r32GB:
                cout << "RAM: 32GB " << endl;
                break;

            case r64GB:
                cout << "RAM: 64GB " << endl;
                break;

            default:
                break;
            }

            switch (allmobiles[i].storage)
            {
            case s16GB:
                cout << "Storage : 16GB " << endl;
                break;

            case s32GB:
                cout << "Storage : 32GB " << endl;
                break;

            case s64GB:
                cout << "Storage : 64GB " << endl;
                break;

            case s128GB:
                cout << "Storage : 128GB " << endl;
                break;

            case s256GB:
                cout << "Storage : 256GB " << endl;
                break;

            case s512GB:
                cout << "Storage : 512GB " << endl;
                break;

            case s1TB:
                cout << "Storage : 1TB " << endl;
                break;

            case s2TB:
                cout << "Storage : 2TB " << endl;
                break;

            default:
                break;
            }

            cout << "price: " << allmobiles[i].price << endl;

            switch (allmobiles[i].color)
            {
            case white:
                cout << "color : white " << endl;
                break;
            case black:
                cout << "color : black " << endl;
                break;
            case Else:
                cout << "color : Else " << endl;
                break;
            }

            cout << "count: " << allmobiles[i].count << endl;
            cout << "sell_number: " << allmobiles[i].sell_number << endl
                 << endl;
        }
    }
}

// choice 8

void most_sold_item(Mobiles *sortmo, int size)
{
    Mobiles *sorted = new Mobiles[size];

    Mobiles max;

    for (int i = 0; i < size; i++)
    {
        max = sortmo[i]; // search maximum

        for (int j = i + 1; j < size; j++)
        {
            if (sortmo[j].sell_number > max.sell_number)
            {
                max = sortmo[j];
            }
        }

        sorted[i] = max;
    }

    print_phones(sorted, size);
}

// file
// choice 9

void save_into_a_file(Mobiles *mobiles, int size)
{
    mobiles = new Mobiles[size];
    ofstream f1("mobile.file", ios::binary);

    if (f1)
    {
        f1 << size;
        for (int i = 0; i < size; ++i)
        {
            f1.write((char *)&mobiles[i], sizeof(Mobiles));
        }
    }

    f1.close();
}

long size_of_file()
{
    long start, end, len;
    ifstream f2("mobile.file", ios::binary);

    start = f2.tellg(); // start =0

    f2.seekg(0, ios::end);
    end = f2.tellg();

    f2.close();

    len = end - start;
    return len;
}

Mobiles *load_from_a_file(long len)
{
    Mobiles *fmobile = new Mobiles;
    int size;

    ifstream f3("mobile.file", ios::binary);

    if (f3)
    {
        f3 >> size;
        while (!f3.eof())
        {
            for (int i = 0; i < size; ++i)
            {
                f3.read((char *)&fmobile[i], len);
            }
        }
    }
    f3.close();
    return fmobile;
}
