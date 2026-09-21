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
