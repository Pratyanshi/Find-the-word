# Find-the-word
C++


Program:

#include <iostream>
#include <fstream>
#include <vector>
#include <iterator>
#include <string>
#include <algorithm>
#include <boost/algorithm/string.hpp>
class TrieNode{
    public:
    unordered_map<char,TrieNode*> mp;
    int isend;
    TrieNode(){
        isend=0;
    }
};

    TrieNode* root;
    Trie() {
        root=new TrieNode;
    }
    
    /** Inserts a word into the trie. */
    void insert(string word) {
        TrieNode* cur=root;
        for(auto& ch:word){
            if(cur->mp.count(ch)==0)    cur->mp[ch]=new TrieNode();
            cur=cur->mp[ch];
        }
        cur->isend++;
    }
    
    /** Returns if the word is in the trie. */
    int count(string word) {
        TrieNode* cur=root;
        for(auto& ch:word){
            if(cur->mp.count(ch)==0)    return false;
            cur=cur->mp[ch];
        }
        return cur->isend;
    }


/*
 * A class to read data from a csv file.
 */
class CSVReader
{
    std::string fileName;
    std::string delimeter;
public:
    CSVReader(std::string filename, std::string delm = ",") :
            fileName(filename), delimeter(delm)
    { }
    // Function to fetch data from a CSV File
    std::vector<std::vector<std::string> > getData();
};
/*
* Parses through csv file line by line and returns the data
* in vector of vector of strings.
*/
std::vector<std::vector<std::string> > CSVReader::getData()
{
    std::ifstream file(fileName);
    std::vector<std::vector<std::string> > dataList;
    std::string line = "";
    // Iterate through each line and split the content using delimeter
    while (getline(file, line))
    {
        std::vector<std::string> vec;
        boost::algorithm::split(vec, line, boost::is_any_of(delimeter));
       for(auto &x:vec) insert(x);
    }
    // Close the File
    file.close();
    return dataList;
}
int main()
{
    // Creating an object of CSVWriter
    CSVReader reader("example.csv");
    // Get the data from CSV File
    std::vector<std::vector<std::string> > dataList = reader.getData();
  string str;
cin>>str
cout<<count(str);
    return 0;
}
