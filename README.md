# 1. Introduction
The Automated Negotiating Agent Competition (ANAC) [1] is an international tournament that has been running since 2010 to bring together researchers from the negotiation community. Our team took part in the Automated Negotiation League (ANL) 2023 [2], where the task is to design a negotiation agent for bilateral negotiation that can learn from every previous encounter while the tournament progresses. The highest-scoring agents based on individual utility and social welfare win.

## 2. Design
The agent is designed to participate in multi-issue negotiations built in Python using the GeniusWeb environment, where each issue has discrete possible values. The critical components of the agent's design are the `OpponentModel` and `IssueEstimator` classes. These components enable the agent to estimate the opponent's preferences and use these estimates to generate bids that are likely to be acceptable to the opponent while maximizing their utility.

## 3. Bidding Strategy
The agent's bidding strategy is to generate bids that maximize its own utility while also considering the predicted utility for the opponent. The utility of an offer for the opponent is predicted using the `get_predicted_utility` method of the `OpponentModel,` which computes a weighted sum of the predicted utilities of the bid's values. Formally, the expected utility  of a bid b is given by:



Where  is the predicted weight of the issue , and  is the predicted utility of the value of the case  in the bid.

## 4. Acceptance Strategy
The acceptance strategy uses a threshold  that decreases linearly over time, ensuring the agent accepts bids with higher utilities for both parties. The agent agrees with an offer if the predicted utility for the opponent () and its utility () are greater than or equal to the current threshold . This approach promotes efficient and mutually beneficial agreements while preventing deadlock and ensuring arrangements can be reached within the given time limit. Using this Acceptance Strategy, we can ensure we will get high Welfare Utility.

## 5. Opponent Model
The opponent's preferences are modeled using an `IssueEstimator` for each issue in the negotiation. The `IssueEstimator` maintains a count of the number of times each value is offered by the opponent and uses these counts to predict the weight of the issue to the opponent and the utility of each value within the issue.

## 6. Learning Method
The agent learns from each negotiation round by updating the `IssueEstimator` for each issue with the values offered in the opponent's bid. This update involves incrementing the count of the provided values and recalculating the predicted weights and utilities. In the `KNN_OpponentModel` variant of the agent, k-nearest neighbors regression is also used to refine the predictions based on the distribution of offered values.

## 7. Summary
The negotiation agent presented in this paper uses a combination of heuristic strategies and machine learning techniques to predict the opponent's preferences and adapt its bidding strategy accordingly. The agent's design allows it to handle complex multi-issue negotiations efficiently, making it suitable for a wide range of applications in automated negotiation. Future work could enhance the agent's performance by incorporating more sophisticated opponent modeling techniques and exploring different bidding and acceptance strategies.

## 8. Reference:
[1] “ANAC2023 - 14th Automated Negotiating Agents Competition”, https://web.tuat.ac.jp/~katfuji/ANAC2023/index.html 
[2] “ANL2023 - Automated Negotiation League 2023”,  https://web.tuat.ac.jp/~katfuji/ANAC2023/genius.html 
