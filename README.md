//program nie dziala w visual studio ze wzgledu na problem z realloc, w code_blocks dziala bez zarzutu
//aby zobaczyc kod poprawnie nalezy wcisnac przycisk raw


#include <stdio.h>
#include <stdbool.h>
#include <time.h>




void swap(int* a, int* b)
{
    int temp = *a;
    *a = *b;
    *b = temp;
}


void insertionSort(int tab[], int n)
{
    register int i, k, j;
    for (i = 1; i < n; i++)
    {
        k = tab[i];
        j = i - 1;
        while (j >= 0 && tab[j] > k) {
            tab[j + 1] = tab[j];
            j = j - 1;
        }
        tab[j + 1] = k;
    }
}

void exchangeSort(int tab[], int n) {
    int i, j;
    for (i = 0; i < (n - 1); i++)
    {
        for (j = (i + 1); j < n; j++)
        {
            if (tab[i] > tab[j])// znak zamienia kolejnosc sortowania
            {
                swap(&tab[i], &tab[j]);
            }
        }
    }
}

void selectionSort(int* tab, int n)
{
    int i, j, k;
    for (i = 0; i < n; i++) {
        k = i;
        for (j = i + 1; j < n; j++)
            if (tab[j] < tab[k])
                k = j;
        swap(&tab[k], &tab[i]);
    }
}



void printArray(int* tab, int n)
{
    int i = 0;
    for (i; i < n; i++)
        printf("%d ", tab[i]);
    printf("\n\n\n");
}

void fullfillArray(int* tab, int n)
{
    int i = 0;
    srand(time(NULL));
    for (i; i < n; i++) {
        tab[i] = rand(time) % 201 - 100;

    }

}




/*
void saveFile(int* tab, char* output, int count)
{
    FILE * fp = fopen(output, "w");
    fprintf(fp, tab);
    fclose(fp);

}

void fullfillRandFile(char* output, int n)
{
    FILE* fp = fopen(output, "w");
    register int i = 0;
    srand(time(0));
    for (i; i < n; i++)
        fprintf(fp, "%d ", rand(time) % 201 - 100);

    printf("\n");



    fclose(fp);

}


void readFile( char* output, int n)
{

    FILE* fp = fopen(output, "r");
    fseek(fp, 0, SEEK_SET);
    int i = 0;
    int value;
    for (i; i < n; i++) {
        fscanf(fp, "%d", &value);
        printf("%d ", value);
    }
    fclose(fp);
}

*/

void almost_sorted_tab(int* tab, int n)
{
    selectionSort(tab, n);
    srand(time(0));
    int i;
    int k=n/100;
    for (i=0; i<n;i+=k)
        tab[k] = rand(time) % 201 - 100;


}





int main()
{
    char input = '0', input2='0';


    int* tab, *tmp;
    tab= (int*)malloc(sizeof(int) * 1);

    int size=1;;


    double elapsed= 0;
    long long after ,before ;
    printf("'i'-Lista instrukcji '0'- wyjscie z programu, '1'-insertionSort, '2'- exchangeSort, '3'- selectionSort\n");
    if (tab!= NULL) {
        do
        {
            scanf(" %c", &input);
            switch (input)
            {
            case '1':
                puts("\nPodaj liczbe elementow w tablicy:(100000 max powyzej trwa wiecej niz 10 sekund)");
                scanf(" %d", &size);
                puts("czy tablica wstepnie posortowana? 1-tak, 0-nie");
                scanf(" %c", &input2);
                if (input2=='0')
                {
                    tmp = (int *) realloc(tab, sizeof(int) * size);

                    if (tmp != NULL)
                    {
                        tab = tmp;
                        fullfillArray(tab, size);
                        before = clock();//mierzenie czasu
                        insertionSort(tab, size);
                        after = clock();
                        printArray(tab, size);
                        elapsed = (double)(after - before) / CLOCKS_PER_SEC;
                        printf("Czas sortowania: %lf\n", elapsed);

                    }

                    else
                        puts("przydzielenie pamięci nie powiodlo sie");

                }
                else if(input2=='1')
                {
                     tmp = (int *) realloc(tab, sizeof(int) * size);

                    if (tmp != NULL)
                    {
                        tab = tmp;
                        fullfillArray(tab, size);
                        almost_sorted_tab(tab,size);
                        before = clock();//mierzenie czasu
                        insertionSort(tab, size);
                        after = clock();
                        printArray(tab, size);
                        elapsed = (double)(after - before) / CLOCKS_PER_SEC;
                        printf("Czas sortowania: %lf\n", elapsed);

                    }

                    else
                        puts("przydzielenie pamięci nie powiodlo sie");

                }
                else
                    puts("Podano zla opcje");

                break;
            case '2':
                puts("\nPodaj liczbe elementow w tablicy:(100000 max powyzej trwa wiecej niz 10 sekund)");
                scanf(" %d", &size);
                puts("czy tablica wstepnie posortowana? 1-tak, 0-nie");
                scanf(" %c", &input2);
                if (input2=='0')
                {
                    tmp = (int *) realloc(tab, sizeof(int) * size);

                    if (tmp != NULL)
                    {
                        tab = tmp;
                        fullfillArray(tab, size);
                        before = clock();//mierzenie czasu
                        exchangeSort(tab, size);
                        after = clock();
                        printArray(tab, size);
                        elapsed = (double)(after - before) / CLOCKS_PER_SEC;
                        printf("Czas sortowania: %lf\n", elapsed);

                    }

                    else
                        puts("przydzielenie pamięci nie powiodlo sie");

                }
                else if(input2=='1')
                {
                     tmp = (int *) realloc(tab, sizeof(int) * size);

                    if (tmp != NULL)
                    {
                        tab = tmp;
                        fullfillArray(tab, size);
                        almost_sorted_tab(tab,size);
                        before = clock();//mierzenie czasu
                        exchangeSort(tab, size);
                        after = clock();
                        printArray(tab, size);
                        elapsed = (double)(after - before) / CLOCKS_PER_SEC;
                        printf("Czas sortowania: %lf\n", elapsed);

                    }

                    else
                        puts("przydzielenie pamięci nie powiodlo sie");

                }
                else
                    puts("Podano zla opcje");

                break;
            case '3':
                 puts("\nPodaj liczbe elementow w tablicy:(100000 max powyzej trwa wiecej niz 10 sekund)");
                scanf(" %d", &size);
                puts("czy tablica wstepnie posortowana? 1-tak, 0-nie");
                scanf(" %c", &input2);
                if (input2=='0')
                {
                    tmp = (int *) realloc(tab, sizeof(int) * size);

                    if (tmp != NULL)
                    {
                        tab = tmp;
                        fullfillArray(tab, size);
                        before = clock();//mierzenie czasu
                        selectionSort(tab, size);
                        after = clock();
                        printArray(tab, size);
                        elapsed = (double)(after - before) / CLOCKS_PER_SEC;
                        printf("Czas sortowania: %lf\n", elapsed);

                    }

                    else
                        puts("przydzielenie pamięci nie powiodlo sie");

                }
                else if(input2=='1')
                {
                     tmp = (int *) realloc(tab, sizeof(int) * size);

                    if (tmp != NULL)
                    {
                        tab = tmp;
                        fullfillArray(tab, size);
                        almost_sorted_tab(tab,size);
                        before = clock();//mierzenie czasu
                        selectionSort(tab, size);
                        after = clock();
                        printArray(tab, size);
                        elapsed = (double)(after - before) / CLOCKS_PER_SEC;
                        printf("Czas sortowania: %lf\n", elapsed);

                    }

                    else
                        puts("przydzielenie pamięci nie powiodlo sie");

                }
                else
                    puts("Podano zla opcje");

                break;

            case 'i':
                puts("'i'-Lista instrukcji '0'- wyjscie z programu, '1'-insertionSort, '2'- exchangeSort, '3'- selectionSort\n");
                break;

            default:
                puts("Podano zla opcje\n");
                break;
            }

        } while (input != '0');

        free(tab);
    }
    else
        puts("blad przydzialu pamieci\n");




    return 0;
}

