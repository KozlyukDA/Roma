#include <iostream>
#include <cstdio>
#include <cstring>
using namespace std;
const size_t MAX_SIZE = 256;
const char* symbols = "*<>?|\"";
int main()
{
    char text[MAX_SIZE];
    cout << "Enter filename" << '\n';
    fgets(text,MAX_SIZE,stdin);
    char* filename = text;
    filename[strlen(filename) - 1] = '\0';
    while(true)
    {
        if(strcspn(filename,symbols) == strlen(filename));
        else
        {
            cout << "Oshibka vvoda";
            break;
        }
        if (strchr(filename,58) != NULL)
        {
            if (strcspn(filename,"\\") == 2)
            {
                if (strcspn(filename,":") == 1)
                {
                    if (isalpha(filename[0])) {}
                    else
                    {
                        cout << "Oshibka vvoda";
                        break;
                    }
                }
                else
                {
                    cout << "Oshibka vvoda";
                    break;
                }
            }
            else
            {
                cout << "Oshibka vvoda";
                break;
            }
        }
        if(strrchr(filename,'.') == nullptr)
            strcat(filename,".txt");
        else
        {
            char* ext = strrchr(filename,'.');
            for(int i = 1;ext[i] != '\0';i++)
                *(ext + i) = char(tolower(*(ext + i)));
            if(strncmp(ext,".txt",4) == 0) ;
            else
            {
                cout << "Oshibka vvoda";
                break;
            }
        }
        FILE* file = fopen(filename,"r+");
        if (file == 0) break;
        fseek(file,0,SEEK_END);
        int file_size = ftell(file);
        char* massive = new char[file_size];
        fseek(file,0,SEEK_SET);
        fread(massive,1,file_size,file);
        massive[file_size] = '\0';
        char stroka[MAX_SIZE];
        cout << "Enter stroka" << '\n';
        fgets(stroka,MAX_SIZE,stdin);
        char* str = stroka;
        *(str + strlen(str) - 1) = '\0';
        int chislo = 0;
        while(*massive != '\0')
        {
            if(strncmp(massive,str,strlen(str)) != 0)
                massive += 1;
            else
            {
                chislo ++;
                massive += 1;
            }
        }
        cout << "Chislo vhozdenyi " << chislo << '\n';
        delete[] massive;
        fclose(file);
        break;
    }
    return 0;
}
