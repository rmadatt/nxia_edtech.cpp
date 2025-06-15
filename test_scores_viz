#include <iostream>
#include <vector>
#include <cmath>
#include <string>
#include <random>
#include <iomanip>
#include <algorithm>

// Calculate the mean of a vector of scores
double calculate_mean(const std::vector<int>& scores) {
    double sum = 0;
    for (int score : scores) sum += score;
    return sum / scores.size();
}

// Calculate the standard deviation of a vector of scores
double calculate_std_dev(const std::vector<int>& scores, double mean) {
    double sum_sq_diff = 0;
    for (int score : scores) sum_sq_diff += (score - mean) * (score - mean);
    return std::sqrt(sum_sq_diff / scores.size());
}

// Categorize a student based on their score relative to mean and standard deviation
std::string categorize(int score, double mean, double std_dev) {
    if (score > mean + std_dev) return "Excellent";
    else if (score < mean - std_dev) return "Needs Improvement";
    else return "Average";
}

// Print a colored bar representing the score
void print_bar(int score, const std::string& category) {
    int num_asterisks = score / 5; // Each asterisk represents 5 points
    std::string color;
    if (category == "Excellent") color = "\033[32m"; // Green
    else if (category == "Average") color = "\033[33m"; // Yellow
    else color = "\033[31m"; // Red
    std::cout << color;
    for (int i = 0; i < num_asterisks; i++) std::cout << "*";
    std::cout << "\033[0m"; // Reset color
}

int main() {
    // Initialize random number generator with a fixed seed for reproducibility
    std::mt19937 gen(42);
    std::uniform_int_distribution<int> dis(0, 100);

    // Generate data for 10 students
    int num_students = 10;
    std::vector<std::pair<std::string, int>> students;
    for (int i = 1; i <= num_students; i++) {
        students.push_back(std::make_pair("Student " + std::to_string(i), dis(gen)));
    }

    // Extract scores for calculations
    std::vector<int> scores;
    for (const auto& student : students) scores.push_back(student.second);

    // Calculate mean and standard deviation
    double mean = calculate_mean(scores);
    double std_dev = calculate_std_dev(scores, mean);

    // Sort students by score in descending order
    std::sort(students.begin(), students.end(), [](const auto& a, const auto& b) {
        return a.second > b.second;
    });

    // Display the bar chart
    std::cout << "Student Test Score Visualization\n";
    std::cout << "--------------------------------\n";
    for (const auto& student : students) {
        std::string category = categorize(student.second, mean, std_dev);
        std::cout << std::left << std::setw(15) << student.first 
                  << " (Score: " << std::setw(3) << student.second << "): ";
        print_bar(student.second, category);
        std::cout << std::endl;
    }

    // Display class statistics
    std::cout << "\nClass Statistics:\n";
    std::cout << "Average: " << std::fixed << std::setprecision(2) << mean << std::endl;
    std::cout << "Standard Deviation: " << std::fixed << std::setprecision(2) << std_dev << std::endl;

    return 0;
}
