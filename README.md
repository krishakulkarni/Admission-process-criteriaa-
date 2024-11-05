#include <stdio.h>
#include <string.h>

#define MAX_GRADE 100

int main() {
    char studentName[50];
    float average;
    float maths, physics, chemistry, english, computerScience;
    int extracurriculars;
    float familyIncome;

    // Minimum average required for the scholarship
    const float scholarshipEligibility = 85.0;

    // For financial aid eligibility
    const float financialAidEligibility = 800000.0;  // Updated to 8 lakh

    // Minimum average for TFWS eligibility
    const float tfwsEligibility = 90.0;

    // Limited seats for EWS
    const int totalEWSSeats = 5;
    int ewsSeatsRemaining = totalEWSSeats;

    printf("Enter the student's name for scholarship eligibility: ");
    fgets(studentName, sizeof(studentName), stdin);
    
    // Remove newline character if present
    studentName[strcspn(studentName, "\n")] = 0;

    // Input marks with validation
    printf("Enter Grade 12 marks for the following subjects (0-100):\n");
    
    printf("Maths: ");
    scanf("%f", &maths);
    while (maths < 0 || maths > MAX_GRADE) {
        printf("Invalid input! Please enter marks between 0 and 100: ");
        scanf("%f", &maths);
    }

    printf("Physics: ");
    scanf("%f", &physics);
    while (physics < 0 || physics > MAX_GRADE) {
        printf("Invalid input! Please enter marks between 0 and 100: ");
        scanf("%f", &physics);
    }

    printf("Chemistry: ");
    scanf("%f", &chemistry);
    while (chemistry < 0 || chemistry > MAX_GRADE) {
        printf("Invalid input! Please enter marks between 0 and 100: ");
        scanf("%f", &chemistry);
    }

    printf("English: ");
    scanf("%f", &english);
    while (english < 0 || english > MAX_GRADE) {
        printf("Invalid input! Please enter marks between 0 and 100: ");
        scanf("%f", &english);
    }

    printf("Computer Science: ");
    scanf("%f", &computerScience);
    while (computerScience < 0 || computerScience > MAX_GRADE) {
        printf("Invalid input! Please enter marks between 0 and 100: ");
        scanf("%f", &computerScience);
    }

    // Calculate average
    average = (maths + physics + chemistry + english + computerScience) / 5;

    // Display average
    printf("\nAverage Marks: %.2f\n", average);

    // Check eligibility for TFWS
    if (average > tfwsEligibility) {
        printf("%s is eligible for the TFWS (Tuition Fee Waiver Scheme) scholarship.\n", studentName);
        return 0; // Exit the program if TFWS is granted
    } 
    
    // Check for EWS only if TFWS is not eligible
    if (average > scholarshipEligibility) {
        printf("%s is not eligible for TFWS. Checking for EWS...\n", studentName);
        
        // Financial background check for EWS
        printf("Enter parent's annual income (in INR): ");
        scanf("%f", &familyIncome);
        
        if (familyIncome < financialAidEligibility) {  // Check if income is less than 8 lakh
            if (ewsSeatsRemaining > 0) {
                printf("%s is eligible for EWS (Economically Weaker Section) benefits.\n", studentName);
                ewsSeatsRemaining--;
            } else {
                printf("No more seats available for EWS benefits.\n");
            }
        } else {
            printf("%s does not qualify for EWS due to financial conditions.\n", studentName);
        }
    } else {
        printf("%s is not eligible for scholarships based on academic performance.\n", studentName);
    }

    // If the student does not qualify for either TFWS or EWS
    if (average < scholarshipEligibility || familyIncome >= financialAidEligibility) {
        printf("%s is not eligible for TFWS or EWS.\n", studentName);
    }

    // Extracurricular achievements check (only if not eligible for any scholarships)
    if (average < scholarshipEligibility) {
        printf("\nEnter number of extracurricular achievements (0-5): ");
        scanf("%d", &extracurriculars);
        if (extracurriculars >= 3) {
            printf("Eligible for extracurricular achievements-based scholarship.\n");
        } else {
            printf("Not eligible for extracurricular achievements-based scholarship.\n");
        }
    }

    return 0;
}
