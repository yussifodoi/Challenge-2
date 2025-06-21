from typing import List
import bisect

class SearchSuggestionSystem:
    def __init__(self, products: List[str]):
        self.products = sorted(products)  # sort lexicographically for binary search

    def getSuggestions(self, searchWord: str) -> List[List[str]]:
        result = []
        prefix = ""
        for char in searchWord:
            prefix += char
            # Find the starting index of the prefix using binary search
            start = bisect.bisect_left(self.products, prefix)
            suggestions = []

            # Check up to the next 3 products from the start index
            for i in range(start, min(start + 3, len(self.products))):
                if self.products[i].startswith(prefix):
                    suggestions.append(self.products[i])
            result.append(suggestions)
        return result
