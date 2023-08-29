mkdir graphql-server-example
cd graphql-server-example
npm init --yes && npm pkg set type="module"
npm install @apollo/server graphql
import { ApolloServer } from '@apollo/server';
import { startStandaloneServer } from '@apollo/server/standalone';

const typeDefs = `#graphql
  
  type Repositories  {
    title: String
    author: String
  }

  
  type Query {
    Repositories : [Repositories ]
  }
`;
const Repositories = [
  {
    title: 'repo name',
    info: 'repo1',
  },
  {
    title: 'repo size',
    ino: 'repo2',
  },
  {
    title: 'repo owner',
   ino: 'repo3',
  },
];
const resolvers = {
  Query: {
    Repositories: () => Repositories,
  },
};

const server = new ApolloServer({
  typeDefs,
  resolvers,
});


const { url } = await startStandaloneServer(server, {
  listen: { port: 4000 },
});

console.log('Server ready at: ${url}`);
npm start
Server ready at: http://localhost:4000/
Visit http://localhost:4000 in your browser, which will open the Apollo Sandbox:
query GetRepositories {
  Repositories {
    repo name
    repo size
    repo owner
    
  }
}
