## Options:

- A Native Testing Library https://github.com/testing-library/native-testing-library
- B React Native Testing Library https://github.com/callstack/react-native-testing-library
- C Enzyme https://www.native-testing-library.com/docs/guide-queries

A and B are similar creatures. They are both integration tests. 

## A/B vs. C:

- A/B runs tests from the perspective of how the users interact with the app, whereas C focuses more on the implementation logic. 
- Therefore, as long as the UI doesn't change much, even when we refactored the code for better performance or using different logic, we won't have massive failing tests as what we see in C. 
- A/B are much easier to set up than C
- C is maintained by AirBnB, which already ditched React Native, so almost no guarantee of future updates for RN
- A/B have getTextByRole, which incorporates the roles in a11y Tech, a good incentive for people to use a11y
	
🎉 So A/B wins the first round. 
And the RN docs recommended both A and B as well: https://reactnative.dev/docs/testing-overview

🧐 But wait, what are the differences between A and B? 

- TLDR: not sure. 
- Slightly longer answer: The library authors couldn't really explain them in detail...Gossip lovers can check out the following links: 
	- (A) says although (B) is also inspired by RTL, but thinks (B) doesn't really adhere to the core values of RTL (https://github.com/testing-library/native-testing-library/issues/1) 
	- (B) says it is just a style preference instead of substantial philosophical differences (https://github.com/callstack/react-native-testing-library/issues/253).
- Further investigations: 
https://medium.com/@brandoncarroll/hello-native-testing-library-91ea326ea0f5
