class BuildPadmaIndex:
    
    def __init__(self, read_from_file=None, debug=False):
    
        self._debug = debug
        
        if isinstance(read_from_file, str):
            self.final_index = self._read_from_file(read_from_file)
        elif read_from_file is None:
            self._null = self._generate_text_index()
        else:
            raise(ValueError('`read_from_file` must be a string that points to a file name.'))
        
    def _read_from_file(self, name):
        
        import pickle
        
        with open(name, 'rb') as f:
            return pickle.load(f)
        
    def _generate_text_index(self):

        from tqdm import tqdm
        
        # get names of files for tokens
        import os
        files = os.listdir('/home/ubuntu/Padma-Data/tokens/')
        
        if self._debug is not False:
            files = files[:self._debug]

        # read tokens into memory
        tokens = {}
        for file in files:

            try:
                tokens[file] = open('/home/ubuntu/Padma-Data/tokens/' + file, 'r').read().split()
            except AttributeError:
                tokens[file] = []

        # create list of all unique tokens
        out = []
        for file in files:
            temp_tokens = tokens[file]
            out += temp_tokens
        word_list = list(set(out))

        # create file-to-id indexes
        self.file_to_id = {}
        self.id_to_file = {}
        for i, file in enumerate(files):
            self.file_to_id[file] = i
            self.id_to_file[i] = file

        # put everything together
        self.final_index = {}
        self.word_set = set(word_list)

        # create key values
        for word in self.word_set:
            self.final_index[word] = {}

        # create values
        for file in tqdm(files):  
            text_set = set(tokens[file])
            
            for word in self.word_set.intersection(text_set):
                
                self.final_index[word][self.file_to_id[file]] = []
            
                locations = list(filter(lambda x: tokens[file][x] == word, range(len(tokens[file]))))
                self.final_index[word][self.file_to_id[file]] += locations
                      
    def word_to_text(self, word):
        
        out = []
        
        for text_id in self.final_index[word].keys():
    
            file = self.id_to_file[text_id]
            text = open('/home/ubuntu/Padma-Data/tokens/' + file, 'r').read()
            
            out.append([file, text])
            
        return out
    
    def word_to_location(self, word):
        
        out = []
        
        for text_id in self.final_index[word].keys():
            
            location = [[text_id, i] for i in self.final_index[word][text_id]]
            
            out.append(location)
            
        return out
    
    def save_to_file(name):
        
        import pickle
        
        with open(name, 'wb') as f:
            pickle.dump(self.final_index, f, pickle.HIGHEST_PROTOCOL)
            
index = BuildPadmaIndex()
index.save_to_file('Padma-Index.pkl')
