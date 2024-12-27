from datetime import datetime
import matplotlib.pyplot as plt
class Candidate:
    def _init_(self, candidate_id, name, party=None): 
        self.candidate_id = candidate_id
        self.name = name
        self.party = party
        self.votes = 0
    def add_vote(self):
        self.votes += 1
class VotingSystem:
    def _init_(self):
        self.candidates = {
            1: Candidate(1, "Konda Sureka", "Congress"),
            2: Candidate(2, "Dasyam VinayBasker", "BRS"),
            3: Candidate(3, "Naaini Rajender", "Independent"),
            4: Candidate(4, "NOTA")  
        }
        self.voted = set()
    def display_candidates(self):
        print("\nAvailable Candidates:")
        for candidate in self.candidates.values():
            party_info = f", Party: {candidate.party}" if candidate.party else ""
            print(f"ID: {candidate.candidate_id}, Name: {candidate.name}{party_info}")
    def cast_vote(self, voter_id):
        if voter_id in self.voted:
            print("You have already voted!")
            return
        print("\n--- Voting Booth ---")
        self.display_candidates()
        try:
            candidate_id = int(input("Enter the ID of the candidate you want to vote for: "))
            if candidate_id not in self.candidates:
                print("Invalid candidate ID! Please try again.")
            else:
                self.candidates[candidate_id].add_vote()
                self.voted.add(voter_id)
                print(f"Vote cast successfully for {self.candidates[candidate_id].name} at {datetime.now()}!")
        except ValueError:
            print("Invalid input! Please enter a valid candidate ID.")
    def display_results(self):
        if not self.candidates:
            print("No candidates available!")
            return
        print("\nElection Results:")
        total_votes = sum(candidate.votes for candidate in self.candidates.values())
        for candidate in self.candidates.values():
            print(f"{candidate.name} (ID: {candidate.candidate_id}): {candidate.votes} votes")
        sorted_candidates = sorted(self.candidates.values(), key=lambda x: x.votes, reverse=True)
        if total_votes > 0:
            majority_threshold = total_votes / 2         
        else:
            majority_threshold = 0
        max_votes = sorted_candidates[0].votes
        winners = [candidate for candidate in sorted_candidates if candidate.votes == max_votes]
        if len(winners) > 1:
            print("It's a tie!")
            for winner in winners:
                print(f"Tied Winner: {winner.name} (ID: {winner.candidate_id}) with {winner.votes} votes")
        else:
            winner = winners[0]
            if len(sorted_candidates) > 1:
                runner_up = sorted_candidates[1]
                margin = winner.votes - runner_up.votes
                print(f"Winner: {winner.name} (ID: {winner.candidate_id}) won with a majority of {margin} votes")
                print(f"Runner-up: {runner_up.name} (ID: {runner_up.candidate_id}) with {runner_up.votes} votes")
            else:
                print(f"Winner: {winner.name} (ID: {winner.candidate_id}) with {winner.votes} votes (majority)")
    def display_results_with_pie_chart(self):
        if not self.candidates:
            print("No candidates available!")
            return
        names = [candidate.name for candidate in self.candidates.values()]
        votes = [candidate.votes for candidate in self.candidates.values()]
        plt.figure(figsize=(7, 7))
        plt.pie(votes, labels=names, autopct='%1.1f%%', startangle=140)
        plt.title("Election Results")
        plt.axis('equal')
        plt.show()

    def add_candidate(self):
        try:
            candidate_id = int(input("Enter candidate ID: "))
            candidate_name = input("Enter candidate name: ")
            candidate_party = input("Enter candidate party (optional): ").strip()
            candidate_party = candidate_party if candidate_party else None
            if candidate_id in self.candidates:
                print("Candidate ID already exists!")
            else:
                self.candidates[candidate_id] = Candidate(candidate_id, candidate_name, candidate_party)
                print("Candidate added successfully!")
        except ValueError:
            print("Invalid input! Candidate ID must be a number.")
system = VotingSystem()
while True:
    print("\n1. Cast Vote\n2. Admin Panel\n3. Exit")
    choice = input("Enter your choice: ")
    if choice == "1":
        voter_id = input("Enter your voter ID: ")
        system.cast_vote(voter_id)
    elif choice == "2":
        admin_password = input("Enter admin password: ")
        if admin_password == "admin123":
            print("\n1. Display Results\n2. Add Candidate\n3. Display Results with Pie Chart\n4. Back")
            admin_choice = input("Enter your choice: ")
            if admin_choice == "1":
                system.display_results()
            elif admin_choice == "2":
                system.add_candidate()
            elif admin_choice == "3":
                system.display_results_with_pie_chart()
            elif admin_choice == "4":
                continue
        else:
            print("Invalid admin password!")
    elif choice == "3":
        print("Exiting...")
        break
    else:
        print("Invalid choice!")
