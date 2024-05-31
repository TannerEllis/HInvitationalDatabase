# HInvitationalDatabase
Database repository for C# Hursty's Invitational
-- Competitors table

CREATE TABLE Competitors (

   CompetitorID INT AUTO_INCREMENT PRIMARY KEY,

   FirstName VARCHAR(255),

   LastName VARCHAR(255),

   NickName VARCHAR(255),

   IsAdmin BOOLEAN DEFAULT false,

   TournamentWinCount INT DEFAULT 0,

   TournamentLossCount INT DEFAULT 0,

   CompetitionCount INT DEFAULT 0

);



-- Tournament table

CREATE TABLE Tournament (

   TournamentID INT AUTO_INCREMENT PRIMARY KEY,

   Year VARCHAR(255),

   StartDate DATE,

   Winner INT,

   SecondPlace INT,

   ThirdPlace INT,

   LastPlace INT,

   IsClosed BOOLEAN DEFAULT false,

   FOREIGN KEY (Winner) REFERENCES Competitors(CompetitorID),

   FOREIGN KEY (SecondPlace) REFERENCES Competitors(CompetitorID),

   FOREIGN KEY (ThirdPlace) REFERENCES Competitors(CompetitorID),

   FOREIGN KEY (LastPlace) REFERENCES Competitors(CompetitorID)

);



-- Games table

CREATE TABLE Games (

   GameID INT AUTO_INCREMENT PRIMARY KEY,

   Name VARCHAR(255),

   IsActive BOOLEAN DEFAULT true,

   PlayCount INT DEFAULT 0

);



-- Tournament Games (many-to-many relationship)

CREATE TABLE TournamentGames (

   TournamentGameID INT AUTO_INCREMENT PRIMARY KEY,

   TournamentID INT,

   GameID INT,

   FOREIGN KEY (TournamentID) REFERENCES Tournament(TournamentID),

   FOREIGN KEY (GameID) REFERENCES Games(GameID)

);



-- Competition Teams

CREATE TABLE CompetitionTeams (

   CompetitionTeamID INT AUTO_INCREMENT PRIMARY KEY,

   TournamentGameID INT,

   Competitor1 INT,

   Competitor2 INT,

   WinCount INT DEFAULT 0,

   FirstPlace INT,

   SecondPlace INT,

   FOREIGN KEY (TournamentGameID) REFERENCES TournamentGames(TournamentGameID),

   FOREIGN KEY (Competitor1) REFERENCES Competitors(CompetitorID),

   FOREIGN KEY (Competitor2) REFERENCES Competitors(CompetitorID),

   FOREIGN KEY (FirstPlace) REFERENCES CompetitionTeams(CompetitionTeamID),

   FOREIGN KEY (SecondPlace) REFERENCES CompetitionTeams(CompetitionTeamID)

   );



-- Tournament Competitors (many-to-many relationship)

CREATE TABLE TournamentCompetitors (

   TournamentCompetitorID INT AUTO_INCREMENT PRIMARY KEY,

   TournamentID INT,

   CompetitorID INT,

   PointsEarned INT DEFAULT 0,

   FOREIGN KEY (TournamentID) REFERENCES Tournament(TournamentID),

   FOREIGN KEY (CompetitorID) REFERENCES Competitors(CompetitorID)

);



-- Tournament Games Matchups

CREATE TABLE TournamentGamesMatchups (

   TournamentGameMatchupID INT AUTO_INCREMENT PRIMARY KEY,

   TournamentGameID INT,

   FirstCompetitionTeamID INT,

   SecondCompetitionTeamID INT,

   Round INT,

   Winner INT,

   FOREIGN KEY (TournamentGameID) REFERENCES TournamentGames(TournamentGameID),

   FOREIGN KEY (FirstCompetitionTeamID) REFERENCES CompetitionTeams(CompetitionTeamID),

   FOREIGN KEY (SecondCompetitionTeamID) REFERENCES CompetitionTeams(CompetitionTeamID),

   FOREIGN KEY (Winner) REFERENCES CompetitionTeams(CompetitionTeamID)

);
