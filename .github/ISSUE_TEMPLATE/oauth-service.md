Feature: OAuth Service Authentication

  As a user,
  I want to log in using third-party services (e.g., Google, GitHub),
  So that I can authenticate easily and securely.

  Background: 
    Given the application is set up with OAuth authentication

  Scenario: User logs in with Google OAuth
    Given the user navigates to the login page
    When the user clicks on "Login with Google"
    And the user is redirected to the Google OAuth provider
    And the user grants permission to the application
    Then the user should be redirected back to the application
    And a valid JWT token should be generated
    And the user should be logged in

  Scenario: User logs in with GitHub OAuth
    Given the user navigates to the login page
    When the user clicks on "Login with GitHub"
    And the user is redirected to the GitHub OAuth provider
    And the user grants permission to the application
    Then the user should be redirected back to the application
    And a valid JWT token should be generated
    And the user should be logged in

  Scenario: User tries to access a protected route without logging in
    Given the user has not logged in
    When the user tries to access a protected route
    Then the user should be redirected to the login page

  Scenario: Token validation middleware works correctly
    Given the user is logged in
    When the user accesses a protected route
    Then the middleware should validate the JWT token
    And the user should be allowed to access the route

  Scenario: Handling OAuth errors
    Given the user clicks on "Login with Google"
    When the user is redirected to the Google OAuth provider
    And the user denies the permission
    Then the user should see an error message saying "Authentication failed"
    And the user should be redirected to the login page

