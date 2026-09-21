# THEmodel
# Block private settings and passwords
.env
secret_tokens.json

# Block active betting slip folders
my_active_slips/
master_tracker_database.db

# Block temporary computer noise files
__pycache__/
*.pyc
.DS_Store
pandas==2.2.2
numpy==1.26.4
requests==2.32.3
beautifulsoup4==4.12.3
# WNBA 1st Quarter Projection Engine

def calculate_wnba_1q_points(player_name, baseline_avg, usage_multiplier, rest_factor, defense_factor):
    """
    Calculates a player's true 1st-quarter points potential based on opening script parameters.
    """
    # Core Formula: Adjust baseline stats by roster shifts and fatigue variables
    adjusted_score = (baseline_avg * usage_multiplier) + rest_factor + defense_factor
    
    print(f"--- 1Q Model Projection for {player_name} ---")
    print(f"Baseline Average: {baseline_avg} PTS")
    print(f"Projected 1Q Output: {round(adjusted_score, 2)} Points")
    
    return round(adjusted_score, 2)

# --- Live Verification Sandbox ---
# Testing Dominique Malonga's high-leverage opening script volume when teammates were ruled out:
if __name__ == "__main__":
    calculate_wnba_1q_points(
        player_name = "Dominique Malonga",
        baseline_avg = 4.5,          # Her usual line set by oddsmakers
        usage_multiplier = 1.25,     # BOOST: Key guards out, opening script funnels inside
        rest_factor = -0.5,          # MINUS: Minor travel fatigue post-FIBA
        defense_factor = 1.0         # PLUS: Opponent lacks elite early rim protection
    )
# NFL Alternative 1st Quarter Rushing Calculator

def project_nfl_1q_rushing(player_name, projected_team_plays, backfield_touch_share, yards_per_carry_matchup):
    """
    Projects 1st-quarter rushing yardage based on opening drive play counts and blocking leverage.
    """
    # Step 1: Calculate how many carries the player gets in the opening 10-12 scripted plays
    projected_carries = projected_team_plays * backfield_touch_share
    
    # Step 2: Multiply carries by the expected yardage efficiency against the opposing defensive line
    projected_yards = projected_carries * yards_per_carry_matchup
    
    print(f"--- NFL 1Q Rushing Projection for {player_name} ---")
    print(f"Projected Opening Script Carries: {round(projected_carries, 1)}")
    print(f"Projected 1Q Yards: {round(projected_yards, 1)} Yards")
    
    return round(projected_yards, 1)

# --- Live Verification Sandbox ---
# Testing Breece Hall's alternate line volume anchor:
if __name__ == "__main__":
    project_nfl_1q_rushing(
        player_name = "Breece Hall",
        projected_team_plays = 12.0,      # Average plays executed in the 1st quarter
        backfield_touch_share = 0.45,     # Commands 45% of early offensive touches
        yards_per_carry_matchup = 4.2     # Projected ground efficiency against opposing defensive front
    )
    # Multi-Sport Parlay Ticket Grader

def evaluate_bet_edge(player_name, sportsbook_line, model_projection, bet_type="OVER"):
    """
    Compares oddsmaker lines against model metrics to output a strategic safety grade.
    """
    # Calculate the percentage difference between the book's line and your calculation
    if bet_type == "OVER":
        edge = model_projection - sportsbook_line
    else:
        edge = sportsbook_line - model_projection
        
    # Grade Evaluation Matrix
    if edge >= 1.5:
        grade = "A (Elite Model Advantage - High Expected Value)"
    elif edge >= 0.5:
        grade = "B (Consistent Script Play - Standard Value)"
    else:
        grade = "C (High Volatility Sweat - Avoid or Lower Units)"
        
    print(f"Bet: {player_name} | Book Line: {sportsbook_line} | Model Projection: {model_projection}")
    print(f"Calculated Edge: {round(edge, 2)} | System Grade: {grade}\n")
    return grade

# --- Test Ticket Run ---
if __name__ == "__main__":
    print("--- RUNNING PARLAY REPORT CARD SIMULATION ---\n")
    # Test Leg 1
    evaluate_bet_edge("Breece Hall 1Q Rushing Yards", 14.5, 22.6, "OVER")
    # Test Leg 2
    evaluate_bet_edge("Aliyah Boston 1Q Points", 3.5, 5.1, "OVER")
    # Test Leg 3
    evaluate_bet_edge("Kayla McBride 1Q Points", 2.5, 1.8, "UNDER")


