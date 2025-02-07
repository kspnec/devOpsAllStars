# Project Architecture

![alt text](assets/project_architechture.png)

# Amazon EventBridge review configs

![alt text](assets/eventBridge_review_schedule.png)

# Project Structure

    game-day-alerts/
     ├── src/
     │   ├── gd_notifications.py          # Main Lambda function code
     ├── policies/
     │   ├── gb_sns_policy.json           # SNS publishing permissions
     │   ├── gd_eventbridge_policy.json   # EventBridge to Lambda permissions
     │   └── gd_lambda_policy.json        # Lambda execution role permissions
     ├── .gitignore
     └── README.md                        # Project Overview
