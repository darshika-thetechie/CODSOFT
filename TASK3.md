import math

# Sample dataset
movies = {
    "Inception": "thief who enters dreams to steal secrets",
    "The Dark Knight": "batman fights joker in gotham",
    "Interstellar": "astronauts travel through a wormhole to save humanity",
    "The Matrix": "hacker discovers the world is a simulation",
    "Avengers: Endgame": "superheroes fight thanos to save the universe",
    "Iron Man": "billionaire builds a high tech suit to fight crime",
    "Shutter Island": "marshal investigates a mysterious hospital",
    "The Prestige": "two magicians compete in dangerous illusions"
}

# Preprocess: convert text into set of words
def tokenize(text):
    return set(text.lower().split())

# Cosine similarity between two texts
def cosine_similarity(text1, text2):
    words1, words2 = tokenize(text1), tokenize(text2)
    common = words1.intersection(words2)
    numerator = len(common)
    denominator = math.sqrt(len(words1) * len(words2))
    if denominator == 0:
        return 0
    return numerator / denominator

# Recommendation function
def recommend(movie_name, num_recommendations=3):
    if movie_name not in movies:
        return ["❌ Movie not found in database."]
    
    target_desc = movies[movie_name]
    scores = {}
    
    for other_movie, desc in movies.items():
        if other_movie != movie_name:
            score = cosine_similarity(target_desc, desc)
            scores[other_movie] = score
    
    # Sort by score (highest first)
    sorted_movies = sorted(scores.items(), key=lambda x: x[1], reverse=True)
    
    return [m for m, s in sorted_movies[:num_recommendations]]

# Example usage
if __name__ == "__main__":
    movie = "Inception"
    print("Because you liked:", movie)
    print("We recommend:", recommend(movie, 3))
