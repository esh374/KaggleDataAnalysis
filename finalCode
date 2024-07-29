#include <iostream>
#include <fstream>
#include <sstream>
#include <vector>
#include <string>
#include <map>
#include <climits>

using namespace std;

struct KickstarterProject {
    string id;
    string name;
    string category;
    string mainCategory;
    string currency;
    string deadline;
    string goal;
    string launched;
    string pledged;
    string state;
    string backers;
    string country;
    string usdPledged;
    string usdPledgedReal;
    string usdGoalReal;

};

vector<string> split(const string& line, char delimiter) {
    vector<string> tokens;
    string token;
    istringstream tokenStream(line);
    while (getline(tokenStream, token, delimiter)) {
        tokens.push_back(token);
    }
    return tokens;
}

void deleteVectors(vector<KickstarterProject>& projects) {
    projects.clear(); // Clear the vector
}

void printProject(const KickstarterProject& project) {
    cout << "ID: " << project.id << endl;
    cout << "Name: " << project.name << endl;
    cout << "Category: " << project.category << endl;
    cout << "Main Category: " << project.mainCategory << endl;
    cout << "Currency: " << project.currency << endl;
    cout << "Deadline: " << project.deadline << endl;
    cout << "Goal: " << project.goal << endl;
    cout << "Launched: " << project.launched << endl;
    cout << "Pledged: " << project.pledged << endl;
    cout << "State: " << project.state << endl;
    cout << "Backers: " << project.backers << endl;
    cout << "Country: " << project.country << endl;
    cout << "USD Pledged: " << project.usdPledged << endl;
    cout << "USD Pledged Real: " << project.usdPledgedReal << endl;
    cout << "USD Goal Real: " << project.usdGoalReal << endl;
    cout << endl;
}

void bubbleSort(vector<pair<string, double> >& arr) {
    int n = arr.size();
    for (int i = 0; i < n - 1; ++i) {
        for (int j = 0; j < n - i - 1; ++j) {
            if (arr[j].second < arr[j + 1].second) {
                swap(arr[j], arr[j + 1]);
            }
        }
    }
}

void calculateSuccessRatesByCountry(const vector<KickstarterProject>& allProjects) {
    vector<pair<string, double> > successRates;

    for (int i = 0; i < allProjects.size(); ++i) {
        const KickstarterProject& project = allProjects[i];
        if (project.state == "successful" || project.state == "failed") {
            bool found = false;
            for (int j = 0; j < successRates.size(); ++j) {
                if (successRates[j].first == project.country) {
                    if (project.state == "successful") {
                        successRates[j].second += 1.0;
                    }
                    found = true;
                    break;
                }
            }
            if (!found && project.state == "successful") {
                successRates.push_back(make_pair(project.country, 1.0));
            }
        }
    }

    for (int i = 0; i < successRates.size(); ++i) {
        const string& country = successRates[i].first;
        double totalProjectsInCountry = 0.0;
        for (int j = 0; j < allProjects.size(); ++j) {
            const KickstarterProject& project = allProjects[j];
            if (project.country == country) {
                totalProjectsInCountry += 1.0;
            }
        }
        successRates[i].second /= totalProjectsInCountry;
    }

    // Sort countries based on success rates
    bubbleSort(successRates);

    // Print sorted list of countries and their success rates
    cout << "Sorted countries based on success rates:" << endl;
    for (int i = 0; i < successRates.size(); ++i) {
        const pair<string, double>& pair = successRates[i];
        cout << "Country: " << pair.first << endl;
        cout << "Success Rate: " << pair.second * 100 << "%" << endl;
    }
}

void calculateSuccessRatesByMainCategory(const vector<KickstarterProject>& allProjects) {
    vector<pair<string, double> > successRates;

    for (int i = 0; i < allProjects.size(); ++i) {
        const KickstarterProject& project = allProjects[i];
        if (project.state == "successful" || project.state == "failed") {
            bool found = false;
            for (int j = 0; j < successRates.size(); ++j) {
                if (successRates[j].first == project.mainCategory) {
                    if (project.state == "successful") {
                        successRates[j].second += 1.0;
                    }
                    found = true;
                    break;
                }
            }
            if (!found && project.state == "successful") {
                successRates.push_back(make_pair(project.mainCategory, 1.0));
            }
        }
    }

    for (int i = 0; i < successRates.size(); ++i) {
        const string& mainCategory = successRates[i].first;
        double totalProjectsInCategory = 0.0;
        for (int j = 0; j < allProjects.size(); ++j) {
            const KickstarterProject& project = allProjects[j];
            if (project.mainCategory == mainCategory) {
                totalProjectsInCategory += 1.0;
            }
        }
        successRates[i].second /= totalProjectsInCategory;
    }

    // Sort main categories based on success rates
    bubbleSort(successRates);

    // Print sorted list of main categories and their success rates
    cout << "Sorted main categories based on success rates:" << endl;
    for (int i = 0; i < successRates.size(); ++i) {
        const pair<string, double>& pair = successRates[i];
        cout << "Main Category: " << pair.first << endl;
        cout << "Success Rate: " << pair.second * 100 << "%" << endl;
    }
}

void calculateSuccessRatesByCategory(const vector<KickstarterProject>& allProjects) {
    // Map to store success rates and total project counts for each category
    map<string, pair<double, int> > categoryStats;

    // Iterate through all projects to calculate success rates and total project counts for each category
    for (const auto& project : allProjects) {
        if (project.state == "successful" || project.state == "failed") {
            // Update the success count for the category
            categoryStats[project.category].first += (project.state == "successful") ? 1.0 : 0.0;
            // Increment the total project count for the category
            categoryStats[project.category].second++;
        }
    }

    // Calculate success rates for each category
    for (auto& category : categoryStats) {
        double successRate = (category.second.second != 0) ? (category.second.first / category.second.second) : 0.0;
        category.second.first = successRate;
    }

    // Custom sorting mechanism based on success rates
    vector<pair<string, pair<double, int> > > sortedCategories(categoryStats.begin(), categoryStats.end());

    for (size_t i = 0; i < sortedCategories.size() - 1; ++i) {
        for (size_t j = 0; j < sortedCategories.size() - i - 1; ++j) {
            if (sortedCategories[j].second.first < sortedCategories[j + 1].second.first) {
                swap(sortedCategories[j], sortedCategories[j + 1]);
            }
        }
    }

    // Print sorted list of categories, their success rates, and total project counts
    cout << "Sorted categories based on success rates:" << endl;
    for (const auto& category : sortedCategories) {
        cout << "Category: " << category.first << endl;
        cout << ", Success Rate: " << (category.second.first * 100) << "%" << endl;
        cout << ", Total Projects: " << category.second.second << endl;
    }
}

void calculateSuccessRatesByBackers(const vector<KickstarterProject>& allProjects) {
    map<string, pair<double, double> > successRates; // Backers Range -> <Total Projects, Successful Projects>

    const pair<int, int> backersRangesData[] = {
        make_pair(0, 100),
        make_pair(101, 200),
        make_pair(201, 300),
        make_pair(301, 400),
        make_pair(401, 500),
        make_pair(501, 1000),
        make_pair(1001, 10000),
        make_pair(10001, 100000),
        make_pair(100001, INT_MAX)
    };

    // Initialize successRates with all backers ranges
    for (int i = 0; i < sizeof(backersRangesData) / sizeof(backersRangesData[0]); ++i) {
        int lowerBound = backersRangesData[i].first;
        int upperBound = backersRangesData[i].second;
        successRates[to_string(lowerBound) + "-" + to_string(upperBound)] = make_pair(0.0, 0.0);
    }

    // Count total and successful projects in each backers range
    for (int i = 0; i < allProjects.size(); ++i) {
        const KickstarterProject& project = allProjects[i];
        if (project.state == "successful" || project.state == "failed") {
            bool found = false;
            for (int j = 0; j < sizeof(backersRangesData) / sizeof(backersRangesData[0]); ++j) {
                int lowerBound = backersRangesData[j].first;
                int upperBound = backersRangesData[j].second;
                int numBackers;
                try {
                    numBackers = stoi(project.backers);
                } catch (const std::invalid_argument&) {
                    // Log error if backers count is invalid
                    cerr << "Error: Invalid backers count for project " << i + 1 << ". Skipping project." << endl;
                    continue; // Skip projects with invalid backers count
                }
                if (numBackers >= lowerBound && numBackers <= upperBound) {
                    string range = to_string(lowerBound) + "-" + to_string(upperBound);
                    successRates[range].first += 1.0; // Increment total projects for range
                    if (project.state == "successful") {
                        successRates[range].second += 1.0; // Increment successful projects for range
                    }
                    found = true;
                    break; // No need to check other ranges for this project
                }
            }
            if (!found) {
                cerr << "Error: No backers range found for project " << i + 1 << ". Skipping project." << endl;
            }
        }
    }

    // Print success rates for each backers range
    cout << "Success rates for each backers range:" << endl;
    for (map<string, pair<double, double> >::iterator it = successRates.begin(); it != successRates.end(); ++it) {
        const string& range = it->first;
        double totalProjectsInRange = it->second.first;
        double successfulProjectsInRange = it->second.second;
        double successRate = successfulProjectsInRange / totalProjectsInRange;
        cout << "Backers Range: " << range << endl;
        cout << "Success Rate: " << successRate * 100 << "%" << endl;
    }
}

void calculateSuccessRatesByGoal(const vector<KickstarterProject>& allProjects) {
    map<string, pair<double, double> > successRates; // Goal Range -> <Total Projects, Successful Projects>

    const pair<int, int> goalRangesData[] = {
        make_pair(1, 100),
        make_pair(101, 200),
        make_pair(201, 300),
        make_pair(301, 400),
        make_pair(401, 500),
        make_pair(501, 600),
        make_pair(601, 700),
        make_pair(701, 800),
        make_pair(801, 900),
        make_pair(901, 1000),
        make_pair(1001, 1100),
        make_pair(1101, 1200),
        make_pair(1201, 1300),
        make_pair(1301, 1400),
        make_pair(1401, 1500),
        make_pair(1501, 1600),
        make_pair(1601, 1700),
        make_pair(1701, 1800),
        make_pair(1801, 1900),
        make_pair(1901, 10000),
        make_pair(10001, 100000),
        make_pair(100001, 1000000),
        make_pair(1000001, 10000000),
        make_pair(10000001, 100000000)
    };

    // Initialize successRates with all goal ranges
    for (int i = 0; i < sizeof(goalRangesData) / sizeof(goalRangesData[0]); ++i) {
        int lowerBound = goalRangesData[i].first;
        int upperBound = goalRangesData[i].second;
        successRates[to_string(lowerBound) + "-" + to_string(upperBound)] = make_pair(0.0, 0.0);
    }

    // Count total and successful projects in each goal range
    for (int i = 0; i < allProjects.size(); ++i) {
        const KickstarterProject& project = allProjects[i];
        if (project.state == "successful" || project.state == "failed") {
            bool found = false;
            for (int j = 0; j < sizeof(goalRangesData) / sizeof(goalRangesData[0]); ++j) {
                int lowerBound = goalRangesData[j].first;
                int upperBound = goalRangesData[j].second;
                int goalAmount;
                try {
                    goalAmount = stoi(project.goal);
                } catch (const std::invalid_argument&) {
                    // Log error if goal amount is invalid
                    cerr << "Error: Invalid goal amount for project " << i + 1 << ". Skipping project." << endl;
                    continue; // Skip projects with invalid goal amount
                }
                if (goalAmount >= lowerBound && goalAmount <= upperBound) {
                    string range = to_string(lowerBound) + "-" + to_string(upperBound);
                    successRates[range].first += 1.0; // Increment total projects for range
                    if (project.state == "successful") {
                        successRates[range].second += 1.0; // Increment successful projects for range
                    }
                    found = true;
                    break; // No need to check other ranges for this project
                }
            }
            if (!found) {
                cerr << "Error: No goal range found for project " << i + 1 << ". Skipping project." << endl;
            }
        }
    }

    // Print success rates for each goal range
    cout << "Success rates for each goal range:" << endl;
    for (map<string, pair<double, double> >::iterator it = successRates.begin(); it != successRates.end(); ++it) {
        const string& range = it->first;
        double totalProjectsInRange = it->second.first;
        double successfulProjectsInRange = it->second.second;
        double successRate = successfulProjectsInRange / totalProjectsInRange;
        cout << "Goal Range: " << range << endl;
        cout << "Success Rate: " << successRate * 100 << "%" << endl;
    }
}

void calculateSuccessRateByProjectNumbers(const vector<KickstarterProject>& allProjects) {
    map<int, vector<KickstarterProject> > projectsByYear;

// Group projects by published year
    for (const auto& project : allProjects) {
        string launchedDate = project.launched;
        int year = stoi(launchedDate.substr(6, 2));
        projectsByYear[2000 + year].push_back(project);
    }

    // Analyze trends for each year
    for (const auto& entry : projectsByYear) {
        int year = entry.first;
        const auto& projects = entry.second;

        double totalProjectsInYear = projects.size();
        double successfulProjects = 0.0;
        double failedProjects = 0.0;

        // Count successful and failed projects in the year
        for (const auto& project : projects) {
            if (project.state == "successful") {
                successfulProjects += 1.0;
            } else if (project.state == "failed") {
                failedProjects += 1.0;
            }
        }

        // Calculate success rate for the year
        double successRate = (totalProjectsInYear > 0) ? (successfulProjects / totalProjectsInYear) * 100 : 0.0;

        // Print analysis results for the year
        cout << "Year: " << year << endl;
        cout << "Total Projects: " << totalProjectsInYear << endl;
        cout << "Successful Projects: " << successfulProjects << endl;
        cout << "Failed Projects: " << failedProjects << endl;
        cout << "Success Rate: " << fixed << setprecision(2) << successRate << "%" << endl;
        cout << "-----------------------------------" << endl;
    }
}

void merge(vector<KickstarterProject>& projects, int start, int mid, int end){
    int n1 = mid - start + 1;
    int n2 = end - mid;
    vector<KickstarterProject> left(n1), right(n2);
    for(int i = 0; i < n1; i++){
        left[i] = projects[start + i];
    }
    for(int i = 0; i < n2; i++){
        right[i] = projects[mid + i + 1];
    }
    int i = 0, j = 0, k = start;
    while(i < n1 && j < n2){
        if(left[i].pledged >= right[j].pledged){
            projects[k] = left[i];
            i++; k++;
        }
        else{
            projects[k] = right[j];
            j++; k++;
        }
    }
    while(i < n1){
        projects[k] = left[i];
        i++; k++;
    }
    while(j < n2){
        projects[k] = right[j];
        j++; k++;
    }
}

void mergesort(vector<KickstarterProject>& projects, int start, int end){
    if(start < end){
        int mid = start + (end - start) / 2;
        mergesort(projects, start, mid);
        mergesort(projects, mid + 1, end);
        merge(projects, start, mid, end);
    }
}

void printTopProject(const vector<KickstarterProject>& projects) {
    if (!projects.empty()) {
        const KickstarterProject& project = projects[0];
        double pledgedAmount = 0.0;
        try {
            pledgedAmount = stod(project.pledged);
        } catch (const std::invalid_argument&) {
            cerr << "Error: Invalid pledged amount for project in country " << project.country << ". Skipping project." << endl;
            return;
        }
        cout << "ID: " << project.id << endl;
        cout << "Name: " << project.name << endl;
        cout << "Category: " << project.category << endl;
        cout << "Pledged: " << pledgedAmount << endl;
    } else {
        cout << "No projects found." << endl;
    }
}

void topFundedProjectsByCountries(const vector<KickstarterProject>& allProjects) {
    // Create a map to store the top funded project for each country
    unordered_map<string, KickstarterProject> topProjectsByCountry;

    // Iterate through all projects to find the top funded project for each country
    for (const auto& project : allProjects) {
        // If the country is not in the map, add the project
        if (topProjectsByCountry.find(project.country) == topProjectsByCountry.end()) {
            topProjectsByCountry[project.country] = project;
        } else {
            // If the project's pledged amount is greater than the current top project for the country, update it
            if (stod(project.pledged) > stod(topProjectsByCountry[project.country].pledged)) {
                topProjectsByCountry[project.country] = project;
            }
        }
    }

    // Print the top funded project for each country
    cout << "Top funded projects by country:" << endl;
    for (const auto& entry : topProjectsByCountry) {
        cout << "Country: " << entry.second.country << endl;
        cout << "ID: " << entry.second.id << endl;
        cout << "Name: " << entry.second.name << endl;
        cout << "Pledged: " << entry.second.pledged << endl;
        cout << endl;
    }
}

void insertionSort(vector<KickstarterProject>& projects) {
    for (size_t i = 1; i < projects.size(); ++i) {
        KickstarterProject key = projects[i];
        int j = i - 1;
        while (j >= 0 && projects[j].pledged < key.pledged) {
            projects[j + 1] = projects[j];
            --j;
        }
        projects[j + 1] = key;
    }
}

void topFundedProjectsByCategories(const vector<KickstarterProject>& allProjects) {
    // Map to store projects grouped by category
    map<string, vector<KickstarterProject> > categoryProjectsMap;

    // Group projects by category
    for (const auto& project : allProjects) {
        categoryProjectsMap[project.category].push_back(project);
    }

    // Iterate over each category
    for (const auto& pair : categoryProjectsMap) {
        const auto& projects = pair.second;
        double maxPledged = 0.0;
        KickstarterProject topProject;

        // Find the project with the maximum pledged amount within the category
        for (const auto& project : projects) {
            try {
                double pledgedAmount = stod(project.pledged);
                if (pledgedAmount > maxPledged) {
                    maxPledged = pledgedAmount;
                    topProject = project;
                }
            } catch (const std::invalid_argument&) {
                // Log error if pledged amount is invalid
                cerr << "Error: Invalid pledged amount for project in category " << pair.first << ". Skipping project." << endl;
            }
        }

        // Print the top funded project for the category
        cout << "Category: " << pair.first << endl;
        if (maxPledged > 0.0) {
            cout << "ID: " << topProject.id << endl;
            cout << "Name: " << topProject.name << endl;
            cout << "Main Category: " << topProject.mainCategory << endl;
            cout << "Pledged: " << maxPledged << endl;
        } else {
            cout << "No projects found." << endl;
        }
        cout << endl;
    }
}

void topFundedProjectsByMainCategory(const vector<KickstarterProject>& allProjects) {
    // Map to store projects grouped by main category
    map<string, vector<KickstarterProject> > mainCategoryProjectsMap;

    // Group projects by main category
    for (const auto& project : allProjects) {
        mainCategoryProjectsMap[project.mainCategory].push_back(project);
    }

    // Iterate over each main category
    for (const auto& pair : mainCategoryProjectsMap) {
        const auto& projects = pair.second;
        double maxPledged = 0.0;
        KickstarterProject topProject;

        // Find the project with the maximum pledged amount within the main category
        for (const auto& project : projects) {
            try {
                double pledgedAmount = stod(project.pledged);
                if (pledgedAmount > maxPledged) {
                    maxPledged = pledgedAmount;
                    topProject = project;
                }
            } catch (const std::invalid_argument&) {
                // Log error if pledged amount is invalid
                cerr << "Error: Invalid pledged amount for project in main category " << pair.first << ". Skipping project." << endl;
            }
        }

        // Print the top funded project for the main category
        cout << "Main Category: " << pair.first << endl;
        if (maxPledged > 0.0) {
            cout << "ID: " << topProject.id << endl;
            cout << "Name: " << topProject.name << endl;
            cout << "Category: " << topProject.category << endl;
            cout << "Pledged: " << maxPledged << endl;
        } else {
            cout << "No projects found." << endl;
        }
        cout << endl;
    }
}

void topFundedProjectsByCurrency(const vector<KickstarterProject>& allProjects) {
    // Map to store projects grouped by currency
    map<string, KickstarterProject> topProjectsByCurrency;

    // Iterate through all projects to find the top pledged project for each currency
    for (const auto& project : allProjects) {
        // Check if the currency already exists in the map
        if (topProjectsByCurrency.find(project.currency) == topProjectsByCurrency.end()) {
            // If the currency is not found, add the project
            topProjectsByCurrency[project.currency] = project;
        } else {
            // If the currency is found, update the project if the current pledged amount is larger
            if (stod(project.pledged) > stod(topProjectsByCurrency[project.currency].pledged)) {
                topProjectsByCurrency[project.currency] = project;
            }
        }
    }

    // Print the top funded project for each currency
    cout << "Top funded projects by currency:" << endl;
    for (const auto& currencyProjectPair : topProjectsByCurrency) {
        const KickstarterProject& project = currencyProjectPair.second;
        cout << "Currency: " << project.currency << endl;
        cout << "ID: " << project.id << endl;
        cout << "Name: " << project.name << endl;
        cout << "Pledged: " << project.pledged << endl;
    }
}

void analyzeTimeTrends(const vector<KickstarterProject>& allProjects) {
    map<int, vector<KickstarterProject> > projectsByYear;

    // Group projects by published year
    for (const auto& project : allProjects) {
        string launchedDate = project.launched;
        int year = stoi(launchedDate.substr(6, 2));
        projectsByYear[2000 + year].push_back(project);
    }

    // Calculate success rates and other metrics for each year
    for (const auto& entry : projectsByYear) {
        int year = entry.first;
        const auto& projects = entry.second;

        double totalProjects = projects.size();
        double successfulProjects = 0.0;
        double totalPledged = 0.0;
        double totalGoal = 0.0;
        map<string, int> categoryCounts;
        map<string, map<string, int> > subcategoryCounts;

        // Count successful projects and calculate total pledged and goal amounts
        for (const auto& project : projects) {
            if (project.state == "successful") {
                successfulProjects += 1.0;
            }
            try {
                totalPledged += stod(project.pledged);
                totalGoal += stod(project.goal);
            } catch (const std::invalid_argument&) {
                // Log error if pledged or goal amount is invalid
                cerr << "Error: Invalid pledged or goal amount for project in year " << year << ". Skipping project." << endl;
            }

            // Count category occurrences
            categoryCounts[project.category]++;

            // Count subcategory occurrences within each category
            subcategoryCounts[project.category][project.mainCategory]++;
        }

        // Calculate success rate
        double successRate = (totalProjects > 0) ? (successfulProjects / totalProjects) * 100 : 0.0;

        // Find the most popular category
        string mostPopularCategory;
        int maxCategoryCount = 0;
        for (const auto& category : categoryCounts) {
            if (category.second > maxCategoryCount) {
                mostPopularCategory = category.first;
                maxCategoryCount = category.second;
            }
        }

        // Find the most popular subcategory within the most popular category
        string mostPopularSubcategory;
        int maxSubcategoryCount = 0;
        for (const auto& subcategory : subcategoryCounts[mostPopularCategory]) {
            if (subcategory.second > maxSubcategoryCount) {
                mostPopularSubcategory = subcategory.first;
                maxSubcategoryCount = subcategory.second;
            }
        }

        // Calculate average pledged amount and average funding goal
        double avgPledged = (totalProjects > 0) ? totalPledged / totalProjects : 0.0;
        double avgGoal = (totalProjects > 0) ? totalGoal / totalProjects : 0.0;

        // Print analysis results for the year
        cout << "Year: " << year << endl;
        cout << "Success Rate: " << fixed << setprecision(2) << successRate << "%" << endl;
        cout << "Most Popular Category: " << mostPopularCategory << endl;
        cout << "Most Popular Subcategory: " << mostPopularSubcategory << endl;
        cout << "Average Pledged Amount: " << avgPledged << endl;
        cout << "Average Funding Goal: " << avgGoal << endl;
        cout << "-----------------------------------" << endl;
    }
}

// Function to perform bubble sort on a vector of pairs
void bubbleSort2(vector<pair<string, int> >& arr) {
    const int n = arr.size();
    for (int i = 0; i < n - 1; ++i) {
        for (int j = 0; j < n - i - 1; ++j) {
            if (arr[j].second < arr[j + 1].second) {
                swap(arr[j], arr[j + 1]);
            }
        }
    }
}

// Function to find the top 20 most popular categories for a specific year
void top20CategoriesForYear(const vector<KickstarterProject>& allProjects, int year) {
    unordered_map<string, int> categoryCounts;

    // Count occurrences of each category for the specified year
    for (const auto& project : allProjects) {
        string launchedDate = project.launched;
        int projectYear = stoi(launchedDate.substr(6, 4)); // Extracting the full year from the date
        if (projectYear == year) {
            categoryCounts[project.category]++;
        }
    }

    // Convert map to vector of pairs
    vector<pair<string, int> > categoryPairs(categoryCounts.begin(), categoryCounts.end());

    // Sort the vector of pairs by count using bubble sort
    bubbleSort2(categoryPairs);

    // Print top 20 categories for the specified year
    cout << "Top 20 Most Popular Categories in " << year << ":" << endl;
    for (int i = 0; i < min(20, static_cast<int>(categoryPairs.size())); ++i) {
        cout << i + 1 << ". " << categoryPairs[i].first << endl;
    }
}

// Function to find the top 20 most popular categories for each year
void top20CategoriesOverYears(const vector<KickstarterProject>& allProjects) {
    // Group projects by year
    map<int, vector<KickstarterProject> > projectsByYear;

    for (const auto& project : allProjects) {
        string launchedDate = project.launched;
        int projectYear = stoi(launchedDate.substr(6, 4)); // Extracting the full year from the date
        projectsByYear[projectYear].push_back(project);
    }

    // Iterate over years and find top 20 categories for each year
    for (const auto& entry : projectsByYear) {
        int year = entry.first;
        const auto& projects = entry.second;
        top20CategoriesForYear(projects, year);
        cout << endl;
    }
}

// Function to find the top 10 countries for a specific year
void top10CountriesForYear(const vector<KickstarterProject>& allProjects, int year) {
    unordered_map<string, int> countryCounts;

    // Count occurrences of each country for the specified year
    for (const auto& project : allProjects) {
        string launchedDate = project.launched;
        int projectYear = stoi(launchedDate.substr(6, 4)); // Extracting the full year from the date
        if (projectYear == year) {
            countryCounts[project.country]++;
        }
    }

    // Convert map to vector of pairs
    vector<pair<string, int> > countryPairs(countryCounts.begin(), countryCounts.end());

    // Sort the vector of pairs by count using bubble sort
    bubbleSort2(countryPairs);

    // Print top 10 countries for the specified year
    cout << "Top 10 Countries in " << year << ":" << endl;
    int count = 1;
    for (const auto& pair : countryPairs) {
        cout << count++ << ". " << pair.first << endl;
        if (count > 10) break; // Stop after printing the top 10 countries
    }
}

// Function to find the top 10 countries for each year
void top10CountriesOverYears(const vector<KickstarterProject>& allProjects) {
    // Group projects by year
    map<int, vector<KickstarterProject> > projectsByYear;

    for (const auto& project : allProjects) {
        string launchedDate = project.launched;
        int projectYear = stoi(launchedDate.substr(6, 4)); // Extracting the full year from the date
        projectsByYear[projectYear].push_back(project);
    }

    // Iterate over years and find top 10 countries for each year
    for (const auto& entry : projectsByYear) {
        int year = entry.first;
        const auto& projects = entry.second;
        top10CountriesForYear(projects, year);
        cout << endl;
    }
}

// Function to find the top 5 main categories for a specific year
void top5MainCategoriesForYear(const vector<KickstarterProject>& allProjects, int year) {
    unordered_map<string, int> mainCategoryCounts;

    // Count occurrences of each main category for the specified year
    for (const auto& project : allProjects) {
        string launchedDate = project.launched;
        int projectYear = stoi(launchedDate.substr(6, 4)); // Extracting the full year from the date
        if (projectYear == year) {
            mainCategoryCounts[project.mainCategory]++;
        }
    }

    // Convert map to vector of pairs
    vector<pair<string, int> > mainCategoryPairs(mainCategoryCounts.begin(), mainCategoryCounts.end());

    // Sort the vector of pairs by count using bubble sort
    bubbleSort2(mainCategoryPairs);

    // Print top 5 main categories for the specified year
    cout << "Top 5 Main Categories in " << year << ":" << endl;
    int count = 1;
    for (const auto& pair : mainCategoryPairs) {
        cout << count++ << ". " << pair.first << endl;
        if (count > 5) break; // Stop after printing the top 5 main categories
    }
}

// Function to find the top 5 main categories for each year
void top5MainCategoriesOverYears(const vector<KickstarterProject>& allProjects) {
    // Group projects by year
    map<int, vector<KickstarterProject> > projectsByYear;

    for (const auto& project : allProjects) {
        string launchedDate = project.launched;
        int projectYear = stoi(launchedDate.substr(6, 4)); // Extracting the full year from the date
        projectsByYear[projectYear].push_back(project);
    }

    // Iterate over years and find top 5 main categories for each year
    for (const auto& entry : projectsByYear) {
        int year = entry.first;
        const auto& projects = entry.second;
        top5MainCategoriesForYear(projects, year);
        cout << endl;
    }
}


void displayMenu() {
    cout << "Menu:" << endl;
    cout << "1. Success Rates" << endl;
    cout << "2. Top Funded" << endl;
    cout << "3. Time Trends" << endl;
    cout << "4. Exit" << endl;
}

void successRatesMenu() {
    cout << "Success Rates Menu:" << endl;
    cout << "1. By Country" << endl;
    cout << "2. By Main Category" << endl;
    cout << "3. By Category" << endl;
    cout << "4. By Backers" << endl;
    cout << "5. By Goal" << endl;
    cout << "6. By Project Numbers" << endl;
}

void topFundedProjectsMenu() {
    cout << "Top Funded Projects Menu:" << endl;
    cout << "1. By Countries" << endl;
    cout << "2. By Categories" << endl;
    cout << "3. By Main Category" << endl;
    cout << "4. By Currency" << endl;
}

void timeAnalysisProjectsMenu() {
    cout << "Time Analysis Menu:" << endl;
    cout << "1. Overall" << endl;
    cout << "2. Top 20 categories" << endl;
    cout << "3. Top 10 Countries" << endl;
    cout << "4. Top 5 MainCategories" << endl;
}

void handleSuccessRatesOption(const vector<KickstarterProject>& allProjects) {
    int option;
    successRatesMenu();
    cout << "Enter your choice: ";
    cin >> option;
    switch (option) {
        case 1:
            calculateSuccessRatesByCountry(allProjects);
            break;
        case 2:
            calculateSuccessRatesByMainCategory(allProjects);
            break;
        case 3:
            calculateSuccessRatesByCategory(allProjects);
            break;
        case 4:
            calculateSuccessRatesByBackers(allProjects);
            break;
        case 5:
            calculateSuccessRatesByGoal(allProjects);
            break;
        case 6:
            calculateSuccessRateByProjectNumbers(allProjects);
            break;
        default:
            cout << "Invalid choice!" << endl;
            break;
    }
}

void handleTopFundedProjectsOption(const vector<KickstarterProject>& allProjects) {
    int option;
    topFundedProjectsMenu();
    cout << "Enter your choice: ";
    cin >> option;
    switch (option) {
        case 1:
            topFundedProjectsByCountries(allProjects);
            break;
        case 2:
            topFundedProjectsByCategories(allProjects);
            break;
        case 3:
            topFundedProjectsByMainCategory(allProjects);
            break;
        case 4:
            topFundedProjectsByCurrency(allProjects);
            break;
        default:
            cout << "Invalid choice!" << endl;
            break;
    }
}

void handleTimeTrendsOption(const vector<KickstarterProject>& allProjects) {
    int option;
    timeAnalysisProjectsMenu();
    cout << "Enter your choice: ";
    cin >> option;
    switch (option) {
        case 1:
            analyzeTimeTrends(allProjects);
            break;
        case 2:
            top20CategoriesOverYears(allProjects);
            break;
        case 3:
            top10CountriesOverYears(allProjects);
            break;
        case 4:
            top5MainCategoriesOverYears(allProjects);
            break;
        default:
            cout << "Invalid choice!" << endl;
            break;
    }
}



int main() {
 ifstream file("/Path/to/dsaProjectData.csv");

    if (!file.is_open()) {
        cerr << "Error opening file!" << endl;
        return 1;
    }

    string line;
    getline(file, line); // Skip header line

    vector<KickstarterProject> successfulProjects;
    vector<KickstarterProject> failedProjects;
    vector<KickstarterProject> allProjects;

    while (getline(file, line)) {
        vector<string> tokens = split(line, ',');
        KickstarterProject project;
        project.id = tokens[0];
        project.name = tokens[1];
        project.category = tokens[2];
        project.mainCategory = tokens[3];
        project.currency = tokens[4];
        project.deadline = tokens[5];
        project.goal = tokens[6];
        project.launched = tokens[7];
        project.pledged = tokens[8];
        project.state = tokens[9];
        project.backers = tokens[10];
        project.country = tokens[11];
        project.usdPledged = tokens[12];
        project.usdPledgedReal = tokens[13];
        project.usdGoalReal = tokens[14];
  
        
        if (project.country != "AT" && project.country != "AU" && project.country != "BE" && project.country != "CH" && 
            project.country != "CA" && project.country != "DE" && project.country != "DK" && project.country != "ES" && 
            project.country != "FR" && project.country != "GB" && project.country != "HK" && project.country != "IE" && 
            project.country != "IT" && project.country != "JP" && project.country != "LU" && project.country != "MX" && 
            project.country != "NL" && project.country != "NO" && project.country != "NZ" && project.country != "SE" && 
            project.country != "SG" && project.country != "US"){
                continue;
            }
        else if (project.state == "successful") {
            successfulProjects.push_back(project);
            allProjects.push_back(project);
        } else if (project.state == "failed") {
            failedProjects.push_back(project);
            allProjects.push_back(project);
        } else {
            cerr << "Warning: Unknown project state '" << project.state << "'. Skipping project." << endl;
        }
    }

    file.close();

    int choice;
     while (true) {
        displayMenu();
        cout << "Enter your choice: ";
        cin >> choice;
        switch (choice) {
            case 1:
                handleSuccessRatesOption(allProjects);
                break;
            case 2:
                handleTopFundedProjectsOption(allProjects);
                break;
            case 3:
                handleTimeTrendsOption(allProjects);
                break;
            case 4:
                cout << "Exiting program." << endl;
                    deleteVectors(allProjects);
                    deleteVectors(successfulProjects);
                   deleteVectors(failedProjects);
                return 0;
            default:
                cout << "Invalid choice!" << endl;
                break;
        }
    }

    deleteVectors(allProjects);
    deleteVectors(successfulProjects);
    deleteVectors(failedProjects);

    return 0;
}
