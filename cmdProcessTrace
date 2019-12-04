/** 
 * File:   zimmerca_hw3.cpp
 * Author: collinzimmerman
 * Copyright: zimmerca@miamioh.edu
 * Created on September 17, 2019, 8:44 PM
 */

#include "zimmerca_hw3.h"
#include <unistd.h>
#include <sys/wait.h>
#include <cstdlib>
#include <iostream>
#include <vector>
#include <string>
#include <iomanip>
#include <algorithm>
#include <fstream>
#include <unordered_map>


using namespace std;
using StrVec = std::vector<std::string>;
using StrStrMap = std::unordered_map<std::string, std::string>;

/**  
 *  This method reads data from a file stream that contains the output
 *  of the ps -fe command and puts the pid and ppid in an unordered map
 *  and the pid and cmd in an unordered map. 
 *  @param is this is the stream from the file that is being read
 *  @param pidPpid this is a reference to an unordered map that 
 *      stores pid and ppid
 *  @param pidCmd this is a reference to an unordered map that
 *      stores pid and cmd
 */
void read(std::ifstream& is, StrStrMap& pidPpid, StrStrMap& pidCmd) {
    std::string line, word, pid, ppid, cmd, cmd2, cmd3;
    while (getline(is, line)) {
        istringstream iss(line);
        iss >> cmd >> pid >> ppid >> cmd >> cmd >> cmd >> cmd;
        std::getline(iss, cmd);
        pidPpid[pid] = ppid;
        pidCmd[pid] = cmd;
    }
}

/**
 *  This method prints the process tree for a given pid using the unordered 
 *  maps and the target pid. The format is "PID\tPPID\tCMD"
 *  @param pidPpid this is a reference to an unordered map that 
 *      stores pid and ppid
 *  @param pidCmd this is a reference to an unordered map that
 *      stores pid and cmd
 *  @param pid this is the target pid
 */
void printProcess(StrStrMap& pidPpid, StrStrMap& pidCmd, string pid) {
    cout << "Process tree for PID: " << pid << endl;
    cout << "PID\tPPID\tCMD" << endl;
    StrVec process;
    while (pid != "1") {
        process.push_back(pid + "\t" + pidPpid.at(pid) + "\t"
                + pidCmd.at(pid));
        pid = pidPpid.at(pid);
    }
    cout << pid << "\t" << pidPpid.at(pid) << "\t" << pidCmd.at(pid) << endl;
    for (size_t i = process.size(); i--;) {
        cout << process[i] << endl;
    }
}

/**
 *  Creates unordered maps and the input stream to read the file.
 *  opens file specified by a command line arg.
 *  calls read and print process methods.
 */
int main(int argc, char** argv) {
    StrStrMap pidPpid, pidCmd;
    std::ifstream input;
    input.open(argv[1]);
    read(input, pidPpid, pidCmd);
    printProcess(pidPpid, pidCmd, argv[2]);
    return 0;
}
