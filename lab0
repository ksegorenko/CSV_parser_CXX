#include <iostream>
#include <string>
#include <fstream>
#include <map>

using namespace std;

bool isLetter(char x){
    return (x >= 'A' && x <= 'Z') || (x >= 'a' && x <= 'z') || (x >= '1' && x <= '9');
}

class Map{
public:
    bool KeysComparing(string key1, string key2){
        return (key1 == key2);
    }

    void AddToMap(string word){
        mp[word]++;
        total_num_of_words++;
    }

    multimap <int, const string*> SortingByChangingKeys()const{
        multimap <int, const string*> multimp;
        for (auto it = mp.begin(); it != mp.end(); it++){
            multimp.insert(make_pair(it->second, &it->first));
        }
        return multimp;
    }

    int TotalWordsCount()const{
        return total_num_of_words;
    }


private:
    int total_num_of_words;
    map <string, int> mp;
};

void OutputToCSV(const multimap <int, const string*> &Sorted, int Total_num){
    string output_path = "output.csv";
    ofstream fout;
    fout.open(output_path);
    if(!fout.is_open()){
        cout << "File opening error!" << endl;
    }

    for(auto it = Sorted.rbegin(); it != Sorted.rend(); it++){
        float freq = (float)(it -> first)/(float)Total_num * 100;
        fout << *it->second << ";" << it -> first << ";" << freq << "%\n";
    }
    fout.close();
}

int main(){
    string input_path = "input.txt";
    ifstream fin;
    fin.open(input_path);
    if(!fin.is_open()){
        cout << "File opening error!" << endl;
    }
    string str;
    string word;
    char symbol = '0';
    Map MyMap;
    while(!fin.eof()) {
        word = "";
        while (isLetter(symbol) && !fin.eof()) {
            word += symbol;
            fin.get(symbol);
        }
        if (!word.empty()){
            MyMap.AddToMap(word);
        }
        fin.get(symbol);
    }

    multimap <int, const string*> Sorted = MyMap.SortingByChangingKeys();
    int Total_num = MyMap.TotalWordsCount();
    OutputToCSV(Sorted, Total_num);

    fin.close();
    return 0;
}
