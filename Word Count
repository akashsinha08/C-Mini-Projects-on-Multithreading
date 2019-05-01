#include<iostream>
#include<fstream>
#include<string>
#include<sstream> 
#include<thread>
#include <set>
#include <vector>
#include <mutex>
using namespace std;
constexpr int lines_per_thread = 50;

string fileName= "/Users/akashpriyadarshi/Downloads/nystory";
std::mutex m;
int count = 0;
void countFreq(int thread_id, string s, string fileName, int beg);
int main(){
  int line_no = 0;
  std::vector<thread> TT ;
  ifstream fin(fileName, std::ifstream::in);
  string s = "Glassdoor";
  string line;
  std::set<int> offsets;
  std::set<int>::iterator it;
  offsets.insert(0);
  char c;
  int chars_read = 0;
  while(fin.get(c)) {
    chars_read++;
    if (c == '.' or c == '?' or c == '!') {
      line_no++;
    }
    if (line_no == lines_per_thread) {
      offsets.insert(chars_read);
      line_no = 0;
    }
  }
  fin.close();
  int thread_id = 0;
  for(it=offsets.begin();it!=offsets.end();it++){
    thread_id++;
    TT.push_back(std::thread(countFreq, thread_id, s, fileName, *it));
  } 
  for(int i=0;i<TT.size(); i++){
    TT[i].join();
  }
  cout<<"The total number of occurrences of the word Glassdoor is = "<< ::count<<endl;
  getchar();
  return 0;
}

void countFreq(int thread_id, string s,string fileName,int start){
    int word_count = 0;
    ifstream fin(fileName,std::ifstream::in);
    fin.seekg(start, fin.beg);
    int glassD_count=0;
    try{
      string line;
      int lines_read = 0;
      auto custom_getline = [](ifstream& fin, string& line, string delim) {
        line.clear();
        char c;
        while ((c = fin.get()) != EOF) {
          if (delim.find(c) != string::npos) break;
          line += c;
        }
        return c != EOF;
      };
      while(custom_getline(fin, line, ".?!")) {
        lines_read++;
        stringstream ss(line);
        string word;
        while (ss >> word) {
          word_count++;
          if(word.find(s) != string::npos)
          {
            std::lock_guard<std::mutex> l(m);
            ++::count;
            ++glassD_count;
          }
        }
        if (lines_read >= lines_per_thread) {
          break;
        }
      }
      {
        std::lock_guard<std::mutex> l(m);
        cout << "Lines read by Thread id "<<thread_id <<" =  "<< lines_read << endl;
      }
    }catch(std::exception& e){
    }
    fin.close();
    {
      std::lock_guard<mutex> l(m);
      cout<<"Number of words scanned by thread " << thread_id << " word count = " << word_count<<endl;
      cout<<"Total number of matches of the input word Glassdoor in the segment by thread " << thread_id <<" =  " << glassD_count<<endl;
    }
}
